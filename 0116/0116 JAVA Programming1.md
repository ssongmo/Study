## Day6. Java Programming (Basic Syntax)
===========================================================

###자바의 컴파일 방식은?

JAVA는 2차적으로 컴파일이 진행된다. VM.. (자세하게 알아보기)

* 컴파일 종류

  * JIT(Just In Time) - 실행 시 최초 한번 기계어로 컴파일, 최초 한번은 속도 저하가 될 수도 있다. (설치하고 실행했을때 컴파일한다.)
  * AOT(Ahead Of Time) - class 파일을 설치시 최초 한번 기계어로 컴파일을 한다. 
                     속도 저하는 없지만 안드로이드 처럼 설치가 명확한 구조에서만 가능.
  * ART - 둘을 합친 방식. 최근에 도입되었다.

  * final - 변수명의 더이상 변경하지 못하게 할 때.
  *string은 기본 자료형이 될수 없다.

##0. 메인 클래스 생성.
-----------------------------------------------
   * 메인 클래스는 반드시 존재해야하며 이곳에서 매소드를 불러들여 사용한다.

```

public class HelloWorld {  //HelloWorld라는 클래스를 생성.

	public static void main(String[] args) { //메인 매소드를 생성. 자료형 : String배열.
		
		HelloWorld hello = new HelloWorld(); //선언. (HelloWorld자료형을 가진 hello에 new(새로운)함수를 선언.)
	}
}  //모든 코딩은 이 클래스 안에서만 진행 되어야 한다.

```
##1. 연산자
-------------------------------------------------
* 값을 콘솔에 출력하는 함수.

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

   * break; : 조건문의 조건을 만족할때까지만 회전하고 매소드를 빠져나온다.
    
   * continue; : 조건문을 만족하면 더 이상 반복문에 진입하지 않는다.


##응용 예제
========================================================

###1. 구구단 

* 이중 for문을 이용.

```
main 함수에 hello.gugudan(int dan);
```

```
public int gugudan(int dan){
		int i,j;	//반복문
		int result =0; //결과값 초기화
		for(i = 1; i<=dan; i++){
			for(j = 1; j<=dan; j++){
				result = i * j;
				System.out.print(i+"x"+j+"="+result+"\t");
			}
			System.out.println("");
		}
		return result;
	}
```

###2. 거스름돈 계산 ( 거스름돈 지폐+동전 갯수 구하기)


* main 함수

```
hello.calculate(10000, 3720); //입력값, 물건의 값.
```

*calculate(int x, int y)함수

```
public void calculate(int payed, int amount){
		int remainder;//거스름돈
		
		int bill_5000=0;
		int bill_1000=0;
		int coin_500=0;
		int coin_100=0;
		int coin_50=0;
		int coin_10=0;
		
		remainder = payed - amount;
		System.out.println("잔돈 :"+ remainder+"원");
		
		bill_5000 = remainder/5000; //오천원 잔돈 갯수 확인
		remainder = remainder - (5000 * bill_5000);// 잔돈 - 오천원권
		bill_1000 = remainder/1000; 
		remainder = remainder - (1000*bill_1000);
		coin_500 = remainder/500;
		remainder = remainder -(500*coin_500);
		coin_100 = remainder/100;
		remainder = remainder - (100*coin_100);
		coin_50 = remainder/50;
		remainder = remainder - (50*coin_50);
		coin_10 = remainder/10;
		remainder = remainder - (10*coin_10);
		
		System.out.println("오천원 "+bill_5000+"개");
		System.out.println("천원 "+bill_1000+"개");
		System.out.println("오백원 "+coin_500+"개");
		System.out.println("백원 "+coin_100+"개");
		System.out.println("오십원 "+coin_50+"개");
		System.out.println("십원 "+coin_10+"개");
	}

```

### 3. int형보다 큰 정수를 입력받은 수까지 모두 더하기. (가우스 공식 이용)


* main 함수

```
//hello.sum();
``` 

* sum 함수

```
public long sum(){
		//1부터 3,333,333,333까지 더하는 함수를 만들고 결과 값을 리턴 받아서 출력하세요.
		long i=0;
		long limit = 3333333333l;
		long sum = (i+limit)*((limit+1)/2);   //가우스 공식 : (1+n)*n/2
		//long sum = (i+limit)*limit/2;
		/*
		long sum = 0;
		for(i=0; i<limit+1; i++){
			sum= sum + i;
		}*/
		System.out.println("합: " + sum);
		return sum;
	
	}
```
