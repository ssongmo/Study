* �̹��ִ� Java�� ���ؼ� ������ �����ӵ��� �����. ������ ������ ������ ������ ��������, 
�׸�ŭ �ڵ��� �����ѽð��� ���Ұ�, �Ϸ翡 14�ð����� �����ϴ� �͵� ���� �������̾���. �̹��ֿ� 
����� Java�� Remind �غ��� �ð��� ���� ���� ���� �� ����.

## Day6. Java Programming (Basic Syntax)
===========================================================

###�ڹ��� ������ �����?

JAVA�� 2�������� �������� ����ȴ�.

* ������ ����

  * JIT(Just In Time) - ���� �� ���� �ѹ� ����� ������, ���� �ѹ��� �ӵ� ���ϰ� �� ���� �ִ�. (��ġ�ϰ� ���������� �������Ѵ�.)
  * AOT(Ahead Of Time) - class ������ ��ġ�� ���� �ѹ� ����� �������� �Ѵ�. 
                     �ӵ� ���ϴ� ������ �ȵ���̵� ó�� ��ġ�� ��Ȯ�� ���������� ����.
  * ART - ���� ��ģ ���. �ֱٿ� ���ԵǾ���.

## ������, ���ǹ�

* ������ - print�� ���� ���, ��Ģ������� �ִ�.

* ���ǹ� - if, switch��
```
if�� - �� ����� ������ ���������� �Ǵ��Ͽ� �ش� �� ���� �ִ� ������ �����Ѵ�.

switch�� - �Էµ� ���� � Ư������ ���Ͽ� �ش� �� ���� �ִ� ������ �����Ѵ�.

```

* �ݺ��� - for, while��(do,while��)
```
for�� - Ư�� �������� ����ŭ �ݺ��ϸ鼭 ������ ������ �����Ѵ�.

while�� - Ư�� ������ ������ �� ������ ������ �����Ѵ�.

```


#Day7. �˰��� ����
==================================
##���� : ���� �׸���
--------------------------------

* �⺻������ Main�� �ҷ��ͼ� �Է°��� �Է� �ް�, �� �żҵ�� ����.
### Main
-------------------------------------

	```
	public static void main(String[] args) {
		DrawPattern dp = new DrawPattern();
		dp.showRectTri(7, "X");
		dp.showReverseTri(5, "A");
		dp.showRectTri2(5, "X");
		dp.showRectTri3(7, "��");
		dp.showRectTri4(6, "��");
		dp.showDiamond(7, "A");
		dp.showDiamond2(11, "A");
	```

### ���簢��
-------------------------------------
count�� unit�� �Է� �޾Ƽ� 1���� �����ؼ� �� ���� count��  ���ڸ�ŭ unit�� ��� �մϴ�. 

 ��) count =5, unit =A
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

### ���簢�� (������)
-------------------------------------
���簢���� �ݴ� �������� ���.
 
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
	      	//���� ���
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

### �Ƕ�̵�
-------------------------------------
�Ƕ�̵带 ���� ���.
 
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

##��ü ����. 

* ��ü: ������ �ڵ�ȭ ���� ��������. ���� �ܰ迡 ����ȭ�� ������ �ڵ��ؾ� �� ���.
* Ŭ���� : ����ȭ �� ��ü�� �ڵ�ȭ ��Ų ��.
* �ν��Ͻ�(��ü): ��ü�� �޸𸮿� �ö� ��Ȳ. Ŭ������ ���ؼ� ��üX, ��üO�� �����Ѵ�.


##�迭

* 1�����迭

	int[]  array= new int[6];

* 2���� �迭

	int[][] array2 = new int[3][3];
		   	       // y,x�� �� ��.
			       //�迭 �Է�
			       //Tip : x���� ���� �����ϰ� x�� ��ȣ �տ� y�� ������ ������ �ش�.

##�ݷ���

Collection�̶� ���� Ÿ���� �������� ������ �����ϱ� ���� �ڹ� ���̺귯���̴�.

�迭�� ����ѵ� �ξ� �� ���� ����.

���� �׸��� Collection���� �ֿ� �������̽��� �������踦 ���� �ش�.


## StringŬ������ �żҵ� (���� ����ϴ�)
```

import java.util.Arrays;

public class Strings {

	public static void main(String[] args) {
		* 1.���ڿ� ��
		//���ڿ�.compareTo(���ڿ�)
		//���ڿ�.equals(���ڿ�)
		//���ڿ�  == ���ڿ�


		String a = "32312321";
		String b = "21223";
		String c = "1232322";

		System.out.println(a.compareTo(b));
		System.out.println(a.compareTo(c));
		
		System.out.println(a.equals(b));
		System.out.println(a.equals(c));
		
		* 2.���ڿ��� �ε��� ��
		System.out.println(a.charAt(2));
		
		* 3. ���ڿ� ��ġ��
		System.out.println(a+b);
		
		* 4. "����"���� �����ϴ� ���ڿ����� Ȯ��
		System.out.println(a.startsWith("23"));
		System.out.println(a.endsWith("22"));
		
		* 5. ã���� �ϴ� ���ڿ��� ���°���� Ȯ��
		System.out.println(a.indexOf("3"));//���ʿ� �˻��Ǵ� �ϳ��� ���� �ּҸ� �˼��ִ�. ã�� ���ڿ��� ������ -1����.
		
		* 6. ���ڿ��� ���� 
		System.out.println(a.length());
		
		* 7. ���ڿ� ����
		System.out.println(a.replace("3","x"));
		
		* 8. ���ڿ� �ڸ���
		System.out.println(a.substring(2,3)); //�ϳ��� �������ָ� 3~������.
		
		* 9. ���ڿ� �и��ϱ�
		String value = "aven/k2kj/34k2/3145";
			String values[] = value.split("/");
			for(String item : values){
				System.out.println(item);
			}
			
		* 10. ����->���ں�ȯ = ����+""
			String ccc = 888+"";
		* 11. ����->���ں�ȯ
			int ddd = Integer.parseInt(ccc); //�� ccc(888)�� ���ڿ��� ���°��� �ƴ϶� ���ڷ� ����. ��Ģ������ ����������.
			long eee = Long.parseLong(ccc);

```

#Day9. ��ü, Ŭ���� 
=================================================

* ��ü��? �Ӽ��� ����� ������ ����� ���Ѵ�. ��ü, ����� ���� Ŭ������ �ִ�.
```
ex)���

�Ӽ�: ��, ��, ��
���: �� = ����. ��= ���Ѵ�, �Դ´�.
```

###opp��?
--------------------------------

 object oriented Programming : ��ü���� ���α׷���. 

�Ӽ��� ����� ���� �ϳ��� ��ü(class)������ ����� ��.

### opp ���� �ܰ�

1.��ȹ 2.�м� 3.���� 4.���� 5.�׽�Ʈ


opp ���� ��Ģ
----------------------------------------

* SOLID
  -SRP - ���� å���� ��Ģ ( � ��ü�� �����̳� ������ �ؾ��ϴ� ������ �ϳ������Ѵ�.)

  -OCP - ����-����Ģ

  -LSP - �������� ��ü ��Ģ

  -DIP - ���� ���� ���� ��Ģ

  -ISP - �������̽� �ݸ� ��Ģ


###������
  
���ٴ� ���� �ڽ��� Ŭ�������� ������ ���� �Ѵٴ� ��.

###���յ�
 
�ٸ� Ŭ������ ������ ���� �Ǵ� ��.

* ������ �������� ���̰� ���յ��� ���ߴ� ���� ����.

##Class �����ϱ�

    Public class Main //Class���� �׻� �빮��.

* Overload = ����Ÿ���̳� ��������� ���Ƶ� ������ �ȿ� 
�Ķ������ ������ ����Ÿ���� �޶���Ѵ�.

* ����������

public : ���� ��Ű�������� ������ �����ϴ�.
protected
private : �������� ��ų��. ���ο����� ����ϴ� ����.

* ���

-�θ��� Class�� �����ͼ� �״�� ����� �� �ִ�.


��ӹ��� ���¿��� �θ�,�ڽĿ� ���� �̸��� ������ ����Ҷ�. 
�ڽ��� ���� ����ϸ� **this**, ��ӹ��� �θ� ������ ����Ҷ� **super**
 
�ڽ��� �θ��� �żҵ带 ����ϰ� ������ @Override�� �ؾ��Ѵ�.
Override�� ���� �����ڸ� �����ϰ� ��� ����.

* ������
�θ��� ������ ���� ������ �⺻���� �ڽĵ��� ���� ������ ������ �� �ִ�.

* Static
//�߰�����

final = ó�� �������� �� �״��. ������ �ȵȴ�.


## Day10. �Խ��� ����� + ���� �����
===========================================================

2�ϵ��� �Խ����� �����, �װ��� ���� ������� �߰��Ͽ���.


**�Խ����� ����� ���� �����ϰ� ���� ����� ��Ŀ� ���� �˾ƺ����� �ϰڴ�.**


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

**IO/NIO�� ���� ����ϴ°�?**

* NIO���

-���� Ŭ���̾�Ʈ ���� ���� �ϳ��� ����� ó�� �۾��� ���� �ɸ��� �ʴ� ��쿡 ���.
 
* IO ���

-���� Ŭ���̾�Ʈ ���� ����, ���۵Ǵ� �����Ͱ� ��뷮�̸鼭 ���������� ó���� �ʿ伺�� �ִ� ���.


*���������� �Խ��� ����⸦ �غ����� �ϰڴ�.*

###����

1. �Խ��ǿ� �� �� ��ɾ �Է��ؼ� ����. ex) Create �Է½� �ۼ�ȭ������..
2. Ŭ������ ����ȭ ��Ű��(Bbs.java,Controller..), ����� ���� ������ �Լ�ȭ ��Ų��. ex) Create(), Read(), Print(), run()...
3. �Լ���� ������ ��� �մ´�. 
4. ������ �����ͺ��̽� ������ ����� �� ��Ʈ�ѷ� �Լ��� ������ �� NIO����� ���� �ؽ�Ʈ ���Ϸ� �����ǵ��� ����.
5. list ��½� ǥ ������� �����Ǿ� ���������� ����.

###����


- **Bbs.java**

* �Խ����� �����ϴ� ����Ʈ�� ����� set,get�Լ��� ����.



```
package com.heosongmoo.bbs;
public class Bbs {
	public Bbs(){  //������ ����.
	}
	
	
	//�۹�ȣ
	//����Ʈ�����
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
* ��� Ŭ������ �Լ��� ȣ���ϴ� ����.
* nio���� ����� ��ı��� �߰�.

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



