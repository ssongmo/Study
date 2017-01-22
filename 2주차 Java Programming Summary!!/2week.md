* 이번주는 Java에 대해서 굉장히 빠른속도로 배웠다. 굉장히 진도가 빠르고 정신이 없었지만, 
그만큼 코딩에 투자한시간도 많았고, 하루에 14시간정도 공부하는 것도 정말 오랜만이었다. 이번주에 
배웠던 Java를 Remind 해보는 시간을 갖는 것이 좋을 것 같다.

## Day6. Java Programming (Basic Syntax)
===========================================================

###자바의 컴파일 방식은?

JAVA는 2차적으로 컴파일이 진행된다.

* 컴파일 종류

  * JIT(Just In Time) - 실행 시 최초 한번 기계어로 컴파일, 최초 한번은 속도 저하가 될 수도 있다. (설치하고 실행했을때 컴파일한다.)
  * AOT(Ahead Of Time) - class 파일을 설치시 최초 한번 기계어로 컴파일을 한다. 
                     속도 저하는 없지만 안드로이드 처럼 설치가 명확한 구조에서만 가능.
  * ART - 둘을 합친 방식. 최근에 도입되었다.

## 연산자, 조건문

* 연산자 - print와 같은 출력, 사칙연산등이 있다.

* 조건문 - if, switch문
```
if문 - 비교 결과가 참인지 거짓인지를 판단하여 해당 블럭 내에 있는 로직을 실행한다.

switch문 - 입력된 값과 어떤 특정값을 비교하여 해당 블럭 내에 있는 로직을 실행한다.

```

* 반복문 - for, while문(do,while문)
```
for문 - 특정 범위내의 값만큼 반복하면서 블럭내의 로직을 실행한다.

while문 - 특정 조건이 만족될 때 블럭내의 로직을 실행한다.

```


#Day7. 알고리즘 패턴
==================================
##부제 : 도형 그리기
--------------------------------

* 기본적으로 Main에 불러와서 입력값을 입력 받고, 각 매소드로 구현.
### Main
-------------------------------------

	```
	public static void main(String[] args) {
		DrawPattern dp = new DrawPattern();
		dp.showRectTri(7, "X");
		dp.showReverseTri(5, "A");
		dp.showRectTri2(5, "X");
		dp.showRectTri3(7, "☆");
		dp.showRectTri4(6, "★");
		dp.showDiamond(7, "A");
		dp.showDiamond2(11, "A");
	```

### 직사각형
-------------------------------------
count와 unit을 입력 받아서 1부터 시작해서 매 라인 count의  숫자만큼 unit을 출력 합니다. 

 예) count =5, unit =A
 A

 AA

 AAA

 AAAA

 AAAAA


```
	public void showRectTri(int count, String unit){
	    int i,j ;
	    for(i=1; i<=count; i++){
		    for(j=1; j<=i;j++){
			    System.out.print(unit);	
		    }
		    System.out.println("");
	    }
	}
```

### 직사각형 (역방향)
-------------------------------------
직사각형을 반대 반향으로 출력.
 
 ex)    
         A

        AA

       AAA

      AAAA

     AAAAA


 ```       
	public void showReverseTri(int count, String unit){
	    int i,j,k ;
	    for(i=1; i<=count; i++){
	      	//공백 출력
		    for(k=count-1; k>=i; k--)
		    {
			    System.out.print(" ");
		    }
		    for(j=1; j<=i;j++){
			    System.out.print(unit);	
		    }
		    System.out.println("");
	    }
		
	}
```

### 피라미드
-------------------------------------
피라미드를 만들어서 출력.
 
 ex)    A

       AAA

      AAAAA

     AAAAAAA
  

```
	public void showRectTri2(int count, String unit){
	    int i,j,k;
	    for (i = 0; i < count; i++) {
	        for (j = 1; j < count - i; j++) {
	            System.out.print(" ");
	        }
	        for (k = 0; k < i * 2 + 1; k++) {
	            System.out.print(unit);
	        }
	        System.out.println();
	    }
	}
````

#Day8. Array, Collection, String Class
==============================================

##객체 지향. 

* 객체: 아직은 코드화 되지 않은상태. 설계 단계에 개념화된 앞으로 코딩해야 할 대상.
* 클래스 : 개념화 된 객체를 코드화 시킨 것.
* 인스턴스(개체): 객체가 메모리에 올라간 상황. 클래스를 통해서 객체X, 개체O를 구현한다.


##배열

* 1차원배열

	int[]  array= new int[6];

* 2차원 배열

	int[][] array2 = new int[3][3];
		   	       // y,x축 이 됨.
			       //배열 입력
			       //Tip : x축을 먼저 정의하고 x축 괄호 앞에 y축 공간을 정의해 준다.

##콜랙션

Collection이란 같은 타입의 참조값을 여러개 저장하기 위한 자바 라이브러리이다.

배열과 비슷한데 훨씬 더 편리한 느낌.

다음 그림은 Collection관련 주요 인터페이스의 계층관계를 보여 준다.


## String클래스의 매소드 (자주 사용하는)
```

import java.util.Arrays;

public class Strings {

	public static void main(String[] args) {
		* 1.문자열 비교
		//문자열.compareTo(문자열)
		//문자열.equals(문자열)
		//문자열  == 문자열


		String a = "32312321";
		String b = "21223";
		String c = "1232322";

		System.out.println(a.compareTo(b));
		System.out.println(a.compareTo(c));
		
		System.out.println(a.equals(b));
		System.out.println(a.equals(c));
		
		* 2.문자열의 인덱스 값
		System.out.println(a.charAt(2));
		
		* 3. 문자열 합치기
		System.out.println(a+b);
		
		* 4. "무엇"으로 시작하는 문자열인지 확인
		System.out.println(a.startsWith("23"));
		System.out.println(a.endsWith("22"));
		
		* 5. 찾고자 하는 문자열이 몇번째인지 확인
		System.out.println(a.indexOf("3"));//최초에 검색되는 하나의 문자 주소만 알수있다. 찾는 문자열이 없으면 -1리턴.
		
		* 6. 문자열의 길이 
		System.out.println(a.length());
		
		* 7. 문자열 변경
		System.out.println(a.replace("3","x"));
		
		* 8. 문자열 자르기
		System.out.println(a.substring(2,3)); //하나만 설정해주면 3~끝까지.
		
		* 9. 문자열 분리하기
		String value = "aven/k2kj/34k2/3145";
			String values[] = value.split("/");
			for(String item : values){
				System.out.println(item);
			}
			
		* 10. 숫자->문자변환 = 숫자+""
			String ccc = 888+"";
		* 11. 문자->숫자변환
			int ddd = Integer.parseInt(ccc); //즉 ccc(888)이 문자열로 들어가는것이 아니라 숫자로 들어간다. 사칙연산이 가능해진다.
			long eee = Long.parseLong(ccc);

```

#Day9. 객체, 클래스 
=================================================

* 객체란? 속성과 기능을 가지는 대상을 말한다. 객체, 기능이 없는 클래스도 있다.
```
ex)사람

속성: 눈, 입, 귀
기능: 눈 = 본다. 입= 말한다, 먹는다.
```

###opp란?
--------------------------------

 object oriented Programming : 객체지향 프로그래밍. 

속성과 기능이 묶인 하나의 객체(class)단위는 만드는 것.

### opp 개발 단계

1.계획 2.분석 3.설계 4.구현 5.테스트


opp 설계 원칙
----------------------------------------

* SOLID
  -SRP - 단일 책임의 원칙 ( 어떤 객체는 수정이나 변경을 해야하는 이유는 하나여야한다.)

  -OCP - 개방-폐쇄원칙

  -LSP - 리스코프 교체 원칙

  -DIP - 의존 관계 역전 원칙

  -ISP - 인터페이스 격리 원칙


###응집도
  
높다는 것은 자신의 클래스에서 재사용을 많이 한다는 것.

###결합도
 
다른 클래스와 연결이 많이 되는 것.

* 개발은 응집도를 높이고 결합도를 낮추는 것이 좋다.

##Class 정의하기

    Public class Main //Class명은 항상 대문자.

* Overload = 리턴타입이나 접근제어가는 같아도 되지만 안에 
파라미터의 개수나 리턴타입이 달라야한다.

* 접근제어자

public : 같은 패키지내에선 접근이 가능하다.
protected
private : 접근제한 시킬때. 내부에서만 사용하는 변수.

* 상속

-부모의 Class를 가져와서 그대로 사용할 수 있다.


상속받은 상태에서 부모,자식에 같은 이름의 변수를 사용할때. 
자식의 것을 사용하면 **this**, 상속받은 부모 변수를 사용할땐 **super**
 
자식이 부모의 매소드를 사용하고 싶을때 @Override를 해야한다.
Override는 접근 제한자를 제외하고 모두 같음.

* 다형성
부모의 정보를 갖고 있으면 기본적인 자식들의 유사 정보를 유추할 수 있다.

* Static
//추가보충

final = 처음 설정해준 값 그대로. 변경이 안된다.


## Day10. 게시판 만들기 + 파일 입출력
===========================================================

2일동안 게시판을 만들고, 그곳에 파일 입출력을 추가하였다.


**게시판을 만들기 전에 간단하게 파일 입출력 방식에 대해 알아보도록 하겠다.**


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

**IO/NIO는 언제 사용하는가?**

* NIO사용

-연결 클라이언트 수가 많고 하나의 입출력 처리 작업이 오래 걸리지 않는 경우에 사용.
 
* IO 사용

-연결 클라이언트 수가 적고, 전송되는 데이터가 대용량이면서 순자적으로 처리될 필요성이 있는 경우.


*본격적으로 게시판 만들기를 해보도록 하겠다.*

###설계

1. 게시판에 들어갈 땐 명령어를 입력해서 들어간다. ex) Create 입력시 작성화면으로..
2. 클래스를 세분화 시키고(Bbs.java,Controller..), 기능을 작은 단위로 함수화 시킨다. ex) Create(), Read(), Print(), run()...
3. 함수들과 메인을 모두 잇는다. 
4. 가상의 데이터베이스 공간을 만들어 각 컨트롤러 함수가 동작할 때 NIO방식을 통해 텍스트 파일로 생성되도록 설정.
5. list 출력시 표 모양으로 정리되어 보여지도록 구현.

###구현


- **Bbs.java**

* 게시판을 구성하는 리스트를 만들고 set,get함수를 설정.



```
package com.heosongmoo.bbs;
public class Bbs {
	public Bbs(){  //생성자 생성.
	}
	
	
	//글번호
	//리스트만들기
	private int no;
	private String title;
	private String content;
	private String author;
	private String datetime;
	
	public int getNo() {
		return no;
	}
	public void setNo(int no) {
		this.no = no;
	}
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	public String getContent() {
		return content;
	}
	public void setContent(String content) {
		this.content = content;
	}
	public String getAuthor() {
		return author;
	}
	public void setAuthor(String author) {
		this.author = author;
	}
	public String getDatetime() {
		return datetime;
	}
	public void setDatetime(String datetime) {
		this.datetime = datetime;
	}
	
}
```

- **MianBbs**
* 모든 클래스와 함수를 호출하는 공간.
* nio파일 입출력 방식까지 추가.

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


* ###Controller.java

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

* ###Util.java

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



