#Day9. 객체, 클래스, 게시판 만들기(1) 
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

###게시판 만들기(1)

###설계

1. 게시판에 들어갈 땐 명령어를 입력해서 들어간다. ex) Create 입력시 작성화면으로..
2. 클래스를 세분화 시키고, 기능을 작은 단위로 함수화 시킨다. ex) Create(), Read(), Print(), run()...
3. 함수들과 메인을 모두 잇는다. 

###구현


- Bbs.java

* 게시판을 구성하는 리스트를 만들고 set,get함수를 설정.

package com.heosongmoo.bbs;

```
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

- Controller

* 각종 명령을 제어하는 클래스. (Create, Update, Read, Delete 함수)

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
	 * 생성
	 * 
	 * @param bbs
	 */
	public void Create(Bbs bbs){
		
		bbs.setDatetime(Util.getDatetime());	
		database.add(bbs);
		
	}
	
	/** 특정 글 읽기
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
	
	/** 전체 읽기
	 * 
	 * @return
	 */
	public ArrayList readAll(){
		
		return database;
	}
	
	/** 수정
	 * 
	 * @param bbs
	 */
	public void update(Bbs bbs){
		//아무것도 안해도 됨.
	}
	
	/** 삭제
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

* 코드가 복잡하고 자구 쓰이는 매소드의 집합소. ex)DatetimeC()

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

* 실행하는 부분

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
	int num=0;
	boolean runFlag = true; //exit용 플래그
	boolean contentFlag = true; //텍스트 입력시 Enter키 적용 플래그
	
		while(runFlag) {
			System.out.println("Welcome!!\n 사용하실 Command를 입력하세요. : create, read, list, exit");
			command = scanner.nextLine();
			
			if(command.equals("create")){
				Bbs bbs = new Bbs();
				
				bbs.setNo(num+1);;
				num++;
								
				System.out.print("작성자를 입력하세요 :    ");
				bbs.setAuthor(scanner.nextLine());
				
				System.out.print("제목을 입력하세요 :   ");
				bbs.setTitle(scanner.nextLine());
				
				print("내용을 입력하세요. ");
				
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
				print("게시판을 종료합니다.");
				runFlag = false;
				}
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

###정리

오늘 처음으로 게시판을 만들어 보았다. 정신없이 하느라 메인 코드가 굉장히 지저분 했고, 가독성도 문제가 있는 것으로 보여진다.
주말까지 깔끔하게 게시판을 만들어보도록 해야겠다..






















