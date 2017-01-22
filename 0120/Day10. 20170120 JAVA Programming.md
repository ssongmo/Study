#�Խ��� �����2 (Update, Delete �߰�), ���� �����

���� �ð��� �Խ����� ��������� �Լ��� �и� �����ʾ� ������ �߾���, update��ɰ� delete����� �߰��Ͽ���.

���� �� �Խ����� New I/O ��, nio ���� ����� ����� �����غ��Ҵ�.

���� �����ϰ� IO�� NIO��Ŀ� ���ؼ� �˾ƺ��ڴ�.


* **IO / NIO**

io vs nio �����͸� ����� �Ѵٴ� ������ ����������, ��Ŀ� �־�� �Ʒ��� ���� �������� �ִ�.
 
| �� | IO | NIO | 
|:-----|:--:|----:|
����� ���| ��Ʈ�� | ä�� |
���۹�� | �͹��� | ���� |
�񵿱��� | �������� | ���� |
���ŷ/�ͺ��ŷ��� | ���ŷ ��ĸ� | �Ѵ� ����|

* nio�� pathó�� :  ��� ����Ʈ �������� �ٷ� ó���Ѵ�.

* ���۶� : HW/SW���� �ӵ� ���̸� �ٿ��ش�. ä���� �⺻������ ���۸� ����Ѵ�.

* ������ ��Ÿ������ ����ִ� inode�� ���� ���� ����µ� path�� ��� ������ ���� ������ �뷮�� ��������.
��������� ��� ��Ÿ������ ���� ���� ���� �ɸ��� ������ path�� �̿��ؼ� �ϴ� ����̴�. 


**���ϰ� ���丮 ����**

//��λ��� ������ ���丮�� ����
Files.createDirectory(path);

//��λ��� ��� ���丮 ����( ���� ��� )
Files.createDirectories(path);


**���� ����, �̵�, ����**
```
Files.copy(fromPath, toPath);
Files.move(fromPath, toPath);
Files.delete(path);
```
**IO/NIO�� ���� ����ϴ°�?**

* NIO���

-���� Ŭ���̾�Ʈ ���� ���� �ϳ��� ����� ó�� �۾��� ���� �ɸ��� �ʴ� ��쿡 ���.
 
* IO ���

-���� Ŭ���̾�Ʈ ���� ����, ���۵Ǵ� �����Ͱ� ��뷮�̸鼭 ���������� ó���� �ʿ伺�� �ִ� ���.


* ###MainBbs.java (�ڵ� ����. (���κκ� ���� �� update,delete,write), nio���� ����� ��ı��� �߰�)

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
	Controller controll = new Controller(); //��Ʈ�ѷ� ��ü ����.
	
	Scanner scanner = new Scanner(System.in);
	Scanner textScanner = new Scanner(System.in);  //�ؽ�Ʈ �Է½� ���� �����ϱ� ���� ��ĳ��
	String command = "";
	
	boolean runFlag = true; //exit�� �÷���
	boolean contentFlag = true; //�ؽ�Ʈ �Է½� EnterŰ ���� �÷���
	
		while(runFlag) {
			System.out.println("Welcome!!\n ����Ͻ� Command�� �Է��ϼ���. : create, read, list, exit");
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
				print("�Խ����� �����մϴ�.");
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
		System.out.print("�ۼ��ڸ� �Է��ϼ��� :    ");
		bbs.setAuthor(scanner.nextLine());
		System.out.print("������ �Է��ϼ��� :   ");
		bbs.setTitle(scanner.nextLine());
		
		print("������ �Է��ϼ���. ");
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
		
		System.out.print("������ �۹�ȣ�� �Է��ϼ��� : ");
		String number = scanner.nextLine();
		int no = Util.getNum(number);
		Bbs bbs = controll.read(no);
		write(scanner, bbs);
		controll.create(bbs);
	}
	
	
	
	public void delete(Scanner scanner, Controller controll){
		System.out.print("������ �� �۹�ȣ�� �Է��ϼ��� : ");
		String number = scanner.nextLine();
		
		int no = Util.getNum(number);
		Bbs bbs = controll.read(no);
		print("�����Ͻðڽ��ϱ�? y/n");
		String yesORno = scanner.nextLine();
		if(yesORno.equals("y")){
			controll.delete(no);
		}else if(yesORno.equals("n")){
			
		}
	}
	
	
	public void read(Scanner scanner, Controller controll){
		//�۹�ȣ
		print("�� ��ȣ�� �Է��ϼ���.");
		int no = Integer.parseInt(scanner.nextLine());
		
		Bbs alreadyRead = controll.read(no);
		if(alreadyRead != null){
			print("�� ��ȣ: " +alreadyRead.getNo());
			print("�۾���: " +alreadyRead.getAuthor());
			print("����: " +alreadyRead.getTitle());
			print("���� " +alreadyRead.getContent());
			print("�ۼ��ð�: "+alreadyRead.getDatetime());
		}
	}
	
	public void list(Controller controll){
		ArrayList<Bbs> list = controll.readAll();
		for(Bbs item : list){
			System.out.print("�۹�ȣ: "+item.getNo()+"  �۾���: "+item.getTitle()+"  ����: "+ item.getTitle());
			print("  �ۼ��ð�: "+item.getDatetime());
			print("����:  "+item.getContent());
		}	
	}
	public void print(String value){
		System.out.println(value);
	}
}
```

* ###Controller.java

-������ �����ͺ��̽� ������ �����ϰ� �� �ȿ� nio������� ���� ������� �־���.

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
			//���Ͽ��� ī��Ʈ�� �о�ͼ� ����
		}else{
			//������ �����ϸ鼭 ���� ��ܿ� ī��Ʈ 0����
			FileUtil.writeNio(DATABASE_DIR, DATABASE_FILE, "0\r\n");
		}
	}
	//Path path = Paths.get(FILE_DATABASE);//�����ɼ�
	//FIles.write(path, serializedBbs.getBytes),
	/**
	 * ����
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
		//��ü�� ��Ʈ������ �ٲ��ִ°�.
		database.add(bbs);
		
	}
	
       ...

```
------------------------

* ###Util.java

 ���� �߰��� Util�� ���� ����� Ŭ������.

```
public class FileUtil {
	private final String FILEROOT = "c:/Users/Songmoo/Desktop/test/";

	public static List<String> readNioLines(String dir, String filename){
			
		Path path = Paths.get(dir, filename); //("���丮���","���ϸ�")
		
		try {
			return Files.readAllLines(path);
			
		}catch(IOException e){
			e.printStackTrace();
		}
		return null;
	}
		
		
	public static String readNio(String dir, String filename){
		Path path = Paths.get(dir, filename); //("���丮���","���ϸ�")
		
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
			//���ٴٵ���ÿɼ�;
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
```	