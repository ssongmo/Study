## Day6. Java Programming (Basic Syntax)
===========================================================

*면접관련 빈도 높은 질문.

###자바의 컴파일 방식은?

JAVA는 2차적으로 컴파일이 진행된다. VM.. (자세하게 알아보기)

*컴파일 종류

  *JIT(Just In Time) - 실행 시 최초 한번 기계어로 컴파일, 최초 한번은 속도 저하가 될 수도 있다. (설치하고 실행했을때 컴파일한다.)
  *AOT(Ahead Of Time) - class 파일을 설치시 최초 한번 기계어로 컴파일을 한다. 
                     속도 저하는 없지만 안드로이드 처럼 설치가 명확한 구조에서만 가능.
  *ART - 둘을 합친 방식. 최근에 도입되었다.

  *final - 변수명의 더이상 변경하지 못하게 할 때.
  *string은 기본 자료형이 될수 없다.

##0. 메인 클래스 생성.
-----------------------------------------------
   *메인 클래스는 반드시 존재해야하며 이곳에서 매소드를 불러들여 사용한다.

```

public class HelloWorld {  //HelloWorld라는 클래스를 생성.

	public static void main(String[] args) { //메인 매소드를 생성. 자료형 : String배열.
		
		HelloWorld hello = new HelloWorld(); //선언. (HelloWorld자료형을 가진 hello에 new(새로운)함수를 선언.)
	}
}  //모든 코딩은 이 클래스 안에서만 진행 되어야 한다.

```
##1. 연산자
-------------------------------------------------
*값을 콘솔에 출력하는 함수.

```
public void print(int value) {
		System.out.println(value);
	}
```

*더하기 ( 이하 사칙연산은 모두 같으니 생략.)

```
public int sum(int a, int b) {
		int result = 0;
		result = a+b;
		
		return result;
	}
```

##2. 조건문
--------------------------------------------------
* if문
   
    비교 결과가 참인지 거짓인지를 판단하여 해당 블럭 내에 있는 로직을 실행한다.

```
public void condition(){
		int a = 15;
		int b = 20;
		int c = 15;
		
		if(a>b){
			System.out.println("a는 b보다 큽니다.");
		} else if(a == b){
			System.out.println("a는 b랑 같습니다.");
		}else{
			System.out.println("a는b보다 작습니다.");
		}
		
		//3항 연산자
		c = (a==15)? 100:0; // a에 15가 들어가면 100을 출력 아니면 0을 출력.
```
	
* switch문

    입력된 값과 어떤 특정값을 비교하여 해당 블럭 내에 있는 로직을 실행한다.

```

switch(a){
			case 1 :
				System.out.println("a는 1입니다.");
				break;
			case 15 :
				System.out.println("a는 15입니다.");
				break;
			case 20 :
				System.out.println("a는 20입니다.");
				break;
			default :
				System.out.println("a는 "+ a +"입니다.");
				break;
			
		}	

```

##3.반복문
------------------------------------------------------
* for문
    
   특정 범위내의 값만큼 반복하면서 블럭내의 로직을 실행한다.

```
for(int i=0; i<10; i++){ // i선언, 범위, 증가 (함수의 실행 순서는 선언, 증가후 범위확인. 즉 1,3,2
			System.out.println("i=" + i);
		}
```
	
* while문
    
   특정 조건이 만족될 때 블럭내의 로직을 실행한다.


```

while(i<limit){
			System.out.println("i2" + i);
			i = i+1;
		}

```

+추가 용어.  

   *break; : 조건문의 조건을 만족할때까지만 회전하고 매소드를 빠져나온다.
    
   *continue; : 조건문을 만족하면 더 이상 반복문에 진입하지 않는다. 
