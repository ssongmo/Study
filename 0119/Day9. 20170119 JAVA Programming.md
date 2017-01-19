#Day9. ��ü, Ŭ����, �Խ��� �����(1) 
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

###�Խ��� �����(1)

###����

1. �Խ��ǿ� �� �� ��ɾ �Է��ؼ� ����. ex) Create �Է½� �ۼ�ȭ������..
2. Ŭ������ ����ȭ ��Ű��, ����� ���� ������ �Լ�ȭ ��Ų��. ex) Create(), Read(), Print(), run()...
3. �Լ���� ������ ��� �մ´�. 

###����


- Bbs.java

* �Խ����� �����ϴ� ����Ʈ�� ����� set,get�Լ��� ����.

package com.heosongmoo.bbs;

```
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

- Controller

* ���� ����� �����ϴ� Ŭ����. (Create, Update, Read, Delete �Լ�)

```
package com.heosongmoo.bbs;

import java.util.ArrayList;
import java.util.Calendar;

public class Controller {
	
	ArrayList<Bbs> database;	//CRUD
	
	public Controller(){
		database = new ArrayList<Bbs>();
	}
	
	/**
	 * ����
	 * 
	 * @param bbs
	 */
	public void Create(Bbs bbs){
		
		bbs.setDatetime(Util.getDatetime());	
		database.add(bbs);
		
	}
	
	/** Ư�� �� �б�
	 * 
	 * @param no
	 */
	public Bbs read(int no){
		for(Bbs item: database){
			if(item.getNo()==no){
				return item;
			}
		}
		return null;
	}
	
	/** ��ü �б�
	 * 
	 * @return
	 */
	public ArrayList readAll(){
		
		return database;
	}
	
	/** ����
	 * 
	 * @param bbs
	 */
	public void update(Bbs bbs){
		//�ƹ��͵� ���ص� ��.
	}
	
	/** ����
	 * 
	 * @param no
	 */
	public void delete(int no){
		for(Bbs item: database){
			if(item.getNo()== no){
				database.remove(item);
			}
		}
	}
	
}
```

- Util.java

* �ڵ尡 �����ϰ� �ڱ� ���̴� �żҵ��� ���ռ�. ex)DatetimeC()

```
package com.heosongmoo.bbs;

import java.util.Calendar;

public class Util {
	public static String getDatetime(){
		Calendar cal = Calendar.getInstance();
		int y = cal.get(Calendar.YEAR);
		int M = cal.get(Calendar.MONTH);
		int d = cal.get(Calendar.DATE);
		int h = cal.get(Calendar.HOUR);
		int m = cal.get(Calendar.MINUTE);
		int s = cal.get(Calendar.SECOND);
		String datetime = y+"-"+(M+1)+"-"+d+" "+h+":"+m+":"+s+"";
		return datetime;
	}
}

```

- mainBbs.java

* �����ϴ� �κ�

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
	int num=0;
	boolean runFlag = true; //exit�� �÷���
	boolean contentFlag = true; //�ؽ�Ʈ �Է½� EnterŰ ���� �÷���
	
		while(runFlag) {
			System.out.println("Welcome!!\n ����Ͻ� Command�� �Է��ϼ���. : create, read, list, exit");
			command = scanner.nextLine();
			
			if(command.equals("create")){
				Bbs bbs = new Bbs();
				
				bbs.setNo(num+1);;
				num++;
								
				System.out.print("�ۼ��ڸ� �Է��ϼ��� :    ");
				bbs.setAuthor(scanner.nextLine());
				
				System.out.print("������ �Է��ϼ��� :   ");
				bbs.setTitle(scanner.nextLine());
				
				print("������ �Է��ϼ���. ");
				
				while(contentFlag == true){
				bbs.setContent(textScanner.nextLine());
					if(command.equals("end")){
						String content ="";
						String content2 ="";
						contentFlag = false;
					}else{
				//	 String stringContents= bbs.setContent(textScanner.nextLine());
					}
				}
				controll.Create(bbs);
				
			}else if(command.equals("read")){
				read(scanner, controll);
				
				
			}else if(command.equals("list")){
				list(controll);
				
			}else if(command.equals("exit")){
				print("�Խ����� �����մϴ�.");
				runFlag = false;
				}
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

###����

���� ó������ �Խ����� ����� ���Ҵ�. ���ž��� �ϴ��� ���� �ڵ尡 ������ ������ �߰�, �������� ������ �ִ� ������ ��������.
�ָ����� ����ϰ� �Խ����� �������� �ؾ߰ڴ�..






















