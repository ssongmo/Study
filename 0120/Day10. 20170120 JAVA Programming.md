#게시판 만들기2 (Update, Delete 추가), 파일 입출력

지난 시간에 게시판을 만들었지만 함수가 분리 되지않아 지저분 했었고, update기능과 delete기능을 추가하였다.

또한 이 게시판을 New I/O 즉, nio 파일 입출력 방식을 적용해보았다.

먼저 간단하게 IO와 NIO방식에 대해서 알아보겠다.


* **IO / NIO**

io vs nio 데이터를 입출력 한다는 목적은 동일하지만, 방식에 있어서는 아래와 같은 차이점이 있다.
 
| 비교 | IO | NIO | 
|:-----|:--:|----:|
입출력 방식| 스트림 | 채널 |
버퍼방식 | 넌버퍼 | 버퍼 |
비동기방식 | 지원안함 | 지원 |
블로킹/넌블로킹방식 | 블로킹 방식만 | 둘다 지원|

* nio의 path처리 :  모두 바이트 형식으로 바로 처리한다.

* 버퍼란 : HW/SW간의 속도 차이를 줄여준다. 채널은 기본적으로 버퍼를 사용한다.

* 파일의 메타정보가 들어있는 inode와 같은 것이 생기는데 path는 경로 정보만 들어가기 때문에 용량이 적어진다.
결론적으로 모든 메타정보에 들어가는 것은 오래 걸리기 때문에 path를 이용해서 하는 방식이다. 


**파일과 디렉토리 생성**

//경로상의 마지막 디렉토리만 생성
Files.createDirectory(path);

//경로상의 모든 디렉토리 생성( 없을 경우 )
Files.createDirectories(path);


**파일 복사, 이동, 삭제**
```
Files.copy(fromPath, toPath);
Files.move(fromPath, toPath);
Files.delete(path);
```
**IO/NIO는 언제 사용하는가?**

* NIO사용

-연결 클라이언트 수가 많고 하나의 입출력 처리 작업이 오래 걸리지 않는 경우에 사용.
 
* IO 사용

-연결 클라이언트 수가 적고, 전송되는 데이터가 대용량이면서 순자적으로 처리될 필요성이 있는 경우.

## 코드 부분

* **MainBbs.java (코드 수정. (메인부분 정리 및 update,delete,write), nio파일 입출력 방식까지 추가)**

```

package com.heosongmoo.bbs;

import java.util.ArrayList;
import java.util.Scanner;

public class MainBbs {

	public static void main(String[] args) {
		MainBbs mainBbs = new MainBbs();
		
		mainBbs.run();
	}
	
	public void run(){
	Controller controll = new Controller(); //컨트롤러 개체 생성.
	
	Scanner scanner = new Scanner(System.in);
	Scanner textScanner = new Scanner(System.in);  //텍스트 입력시 따로 저장하기 위한 스캐너
	String command = "";
	
	boolean runFlag = true; //exit용 플래그
	boolean contentFlag = true; //텍스트 입력시 Enter키 적용 플래그
	
		while(runFlag) {
			System.out.println("Welcome!!\n 사용하실 Command를 입력하세요. : create, read, list, exit");
			command = scanner.nextLine();
			
			if(command.equals("create")){
				create(scanner, controll);
				
			}else if(command.equals("read")){
				read(scanner, controll);
				
				
			}else if(command.equals("list")){
				list(controll);
			
			}else if(command.equals("update")){
				update(scanner, controll);
			
			}else if(command.equals("delete")){
				delete(scanner, controll);
				
			}else if(command.equals("exit")){
				print("게시판을 종료합니다.");
				runFlag = false;
				}
			}
		}

	public void create(Scanner scanner, Controller controll){
		Bbs bbs = new Bbs();

		write(scanner, bbs);
		controll.create(bbs);
		
	}
	
	
	public void write(Scanner scanner, Bbs bbs){
	
		boolean contentFlag = true;
		System.out.print("작성자를 입력하세요 :    ");
		bbs.setAuthor(scanner.nextLine());
		System.out.print("제목을 입력하세요 :   ");
		bbs.setTitle(scanner.nextLine());
		
		print("내용을 입력하세요. ");
			String content ="";
			String contents2 ="";
			
			while(contentFlag == true){
				contents2 = scanner.nextLine();
			
				if(contents2.equals("quit")){
					contentFlag = false;
				}else{
			content = content+contents2 + "\n";
				}
			}
			bbs.setContent(content);
	}
	
	public void update(Scanner scanner, Controller controll){
		
		System.out.print("수정할 글번호를 입력하세요 : ");
		String number = scanner.nextLine();
		int no = Util.getNum(number);
		Bbs bbs = controll.read(no);
		write(scanner, bbs);
		controll.create(bbs);
	}
	
	
	
	public void delete(Scanner scanner, Controller controll){
		System.out.print("삭제할 할 글번호를 입력하세요 : ");
		String number = scanner.nextLine();
		
		int no = Util.getNum(number);
		Bbs bbs = controll.read(no);
		print("삭제하시겠습니까? y/n");
		String yesORno = scanner.nextLine();
		if(yesORno.equals("y")){
			controll.delete(no);
		}else if(yesORno.equals("n")){
			
		}
	}
	
	
	public void read(Scanner scanner, Controller controll){
		//글번호
		print("글 번호를 입력하세요.");
		int no = Integer.parseInt(scanner.nextLine());
		
		Bbs alreadyRead = controll.read(no);
		if(alreadyRead != null){
			print("글 번호: " +alreadyRead.getNo());
			print("글쓴이: " +alreadyRead.getAuthor());
			print("제목: " +alreadyRead.getTitle());
			print("내용 " +alreadyRead.getContent());
			print("작성시간: "+alreadyRead.getDatetime());
		}
	}
	
	public void list(Controller controll){
		ArrayList<Bbs> list = controll.readAll();
		for(Bbs item : list){
			System.out.print("글번호: "+item.getNo()+"  글쓴이: "+item.getTitle()+"  제목: "+ item.getTitle());
			print("  작성시간: "+item.getDatetime());
			print("내용:  "+item.getContent());
		}	
	}
	public void print(String value){
		System.out.println(value);
	}
}
```

* **Controller.java**

-가상의 데이터베이스 공간을 설계하고 그 안에 nio방식으로 파일 입출력을 넣었다.

```
package com.heosongmoo.bbs;

import java.nio.file.Files;
import java.nio.file.LinkOption;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.Calendar;

public class Controller {
	
	public static final String DATABASE_DIR = "c:/Users/Songmoo/Desktop/test/";
	public static final String DATABASE_FILE = "database.txt";
	public static final String DATABASE_INDEX = "database.txt";
	String DB_SEPARATOR = "^";
	
	ArrayList<Bbs> database;	//CRUD
	int count; 
	public Controller(){
		database = new ArrayList<Bbs>();
		createDatabase();
		count = 0;
	}
	
	private void createDatabase(){
		Path path = Paths.get(DATABASE_DIR, DATABASE_FILE);
		if(Files.exists(path,LinkOption.NOFOLLOW_LINKS)){
			//파일에서 카운트를 읽어와서 세팅
		}else{
			//파일을 생성하면서 제일 상단에 카운트 0세팅
			FileUtil.writeNio(DATABASE_DIR, DATABASE_FILE, "0\r\n");
		}
	}
	//Path path = Paths.get(FILE_DATABASE);//생성옵션
	//FIles.write(path, serializedBbs.getBytes),
	/**
	 * 생성
	 * 
	 * @param bbs
	 */
	public void create(Bbs bbs){
		count = count +1;
		bbs.setNo(count);
		bbs.setDatetime(Util.getDatetime());
		
		String serializedBbs = bbs.getNo()
				+DB_SEPARATOR + bbs.getAuthor()
				+DB_SEPARATOR + bbs.getTitle()
				+DB_SEPARATOR + bbs.getContent()
				+"\r\n";
		
		FileUtil.writeNio(DATABASE_DIR, DATABASE_FILE, content);
		//객체를 스트링으로 바꿔주는거.
		database.add(bbs);
		
	}
	
       ...

```
------------------------

* **Util.java**

 새로 추가된 Util은 파일 입출력 클래스다.

```
public class FileUtil {
	private final String FILEROOT = "c:/Users/Songmoo/Desktop/test/";

	public static List<String> readNioLines(String dir, String filename){
			
		Path path = Paths.get(dir, filename); //("디렉토리경로","파일명")
		
		try {
			return Files.readAllLines(path);
			
		}catch(IOException e){
			e.printStackTrace();
		}
		return null;
	}
		
		
	public static String readNio(String dir, String filename){
		Path path = Paths.get(dir, filename); //("디렉토리경로","파일명")
		
		try {
			byte rawData[] = Files.readAllBytes(path);
			
			String content = new String(rawData, StandardCharsets.UTF_8);
		} catch (IOException e) {
		
			e.printStackTrace();
		}
		return "";
	}
	
	public static void writeNio(String dir, String filename, String content){
		
		Path path = Paths.get(dir, filename);
		try {
			Files.write(path, content.getBytes(StandardCharsets.UTF_8),
					StandardOpenOption.CREATE, StandardOpenOption.APPEND);
			//스텐다드오플옵션;
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
```	
