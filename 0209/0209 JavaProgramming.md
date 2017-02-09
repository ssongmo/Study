
## Design Patteren -Part.1
 ### Singleton
 * 싱글턴 패턴은 자원을 공유하기 위한 목적으로 사용한다.
 * multi=Thread 환경에서는 아래 로직에 동기화를 추가해야한다.

 ```
public class Singleton{
	//자신을 담아두는 변수 공간.
	private static Singleton instance = null;

	private Singleton(){
	}
	public static Singleton getInstance(){
		if(instance == null){
			instance = new Singleton();
		}
		return instance;

        public String name = "";
    }
}

```

  위의 소스 코드와 같이 Singleton에 접근하지 못하게 private으로 정의 해주면 Main에선 new를 통해 접근 할 수 없다.

```
  public static void main(String[] args) {
  		// 1. 싱글턴 패턴 사용해보기.
  		Singleton single1 = Singleton.getInstance();
      ...
```
new가 아닌 getInstance메소드를 통해서 호출 할 수 있으며, 다른 클래스, 안드로이드에선 다른 액티비티들 간에 데이터를 공유할 수 있게 된다.

---
### Multiton

* 싱글턴과 반대되는 개념이지만 new라는 의존성을 제거해준다는 장점이 있다.

```
public class Multiton {

 private Multiton(){
 //접근하지 못하게 생성자를 블록.
 }

 //생성함수 제공.
 public static Multiton newInstance(){
   return new Multiton();
 }

 public String name = "";
 ```
 싱글톤과 동일하게 접근하지 못하게 private으로 블록하지만 new를 해서 선언하는 것과 크게 다르지 않다. 다만 차이점은이자 장점은 의존성을 줄여준다는 것이다.

 ```
 // 2. 멀티턴 패턴 사용해보기. 사실상 의존성을 떨어뜨리기위해 사용함. new랑 별 차이가 없음.
		Multiton multi1 = Multiton.newInstance();
		Multiton multi2 = Multiton.newInstance();
      ...

  ```
  싱글톤과 동일한 방식으로 출력해 보았다.

  * Tip : 싱글톤과 멀티톤을 동시에 사용할 수 있기도 하다.
  예) single1, single2, single3를 사용한다면, single1,2를 싱글톤으로, single3을 멀티톤으로 설정한다면 1,2는 동일한 데이터 주소를 사용하고, 3은 다른 주소를 가지게 된다.

---
## Proxy
* 대행자로써 중간에 다른 기능 또는 요구사항을 처리한 후 클라이언트 요청에 대한 원본데이터 변형하지 않고 그대로 전달한다.

```
public class Proxy {
	private Proxy(){ }

	private static Proxy instance = null;

	public static Proxy getInstance(){
		if(instance == null){
			instance = new Proxy();
		}
		return instance;
	}

	public static Bbs getBbs(int bbsno){
		Bbs bbs = Database.readBbs(bbsno);

		//원본 데이터는 변형하지 않고, 조회수를 증가시켜준다.
		//Visit과 Bbs 를 분리시켜 원본데이터를 유지시키는 방식이 Proxy 패턴이다.
		Visit visit = new Visit();
		visit.increase(bbsno);
		return bbs;
	}
}
```
Databas에 Bbs 데이터를 셋팅하고 visit()에서 따로 count를 증가시키는 방식이다.
```
public class Visit {
	int no;
	int count = 0;
	public void increase(int bbsno) {
		no = bbsno;
		count = count+1;//database save...etc
	}
}
```
---
### Decorator
 Proxy와 유사하지만 데이터의 변경 및 삭제가 발생한다면 Decorator라고 한다.
 간단하게 정리하자면 데이터를 가공하게 되면 Decorator, 정류장처럼 지나가는것이면 Proxy이다.
---


### Template Method
협업을 할때 많이 사용되는 방식으로써, 부모 클래스인 추상클래스에 구현된 함수가 자식 클래스에서 구현된 추상매서드를 구현한 방식. 즉, 부모클래스에 정의된 추상클래스를(구현될 메소드) 모아두고 그것을 자식 클래스가 사용하는 방식.

![스크린샷 2017-02-09 오후 4.46.49](http://i.imgur.com/QVLz0PS.png=100x20)

* [템플릿 매소드에 Play()함수를 생성]

![스크린샷 2017-02-09 오후 4.47.09](http://i.imgur.com/twdTGQS.png=100x20)
![스크린샷 2017-02-09 오후 4.47.23](http://i.imgur.com/MK3k2yJ.png=100x20)
* [점프할 동물을 설정]

![스크린샷 2017-02-09 오후 4.47.42](http://i.imgur.com/bgJhV47.png=100x20)
* [메인에서 호출]

**main에서 .play()를 사용하면 jump를 하는것을 볼 수 있다.**

---
### Factory Method

 * 인스턴스를 생성하는 인터페이스를 미리 정의하고, 인스턴스의 생성을 서브클래스에게 위함하는 패턴.
 * 확장한 부모클래스의 매서드를 오버라이드해서 반환해준다.
 행위 패턴인 Template Method 패턴은 중복을 없애고 코드 재사용을 위해 객체를 사용하는 방법에 초점을 맞추고 있는 반면, Factory Method 패턴은  생성하고자 하는 객체의 클래스(Product)와 이를 생성하는 클래스(Factory)의 인터페이스만 공개하여 재사용성을 높인다.
 *Factory Method 패턴은  생성하고자 하는 객체의 클래스(Product)와 이를 생성하는 클래스(Factory)의 인터페이스만 공개하여 재사용성을 높입니다.*

---
 ### Strategy

 * 탬플릿 패턴과 유사한데, 탬플릿패턴이 상속을 이용하는 반면 Strategy패턴은 객체 주입을 통해 다양한 결과를 도출할 수 있다. 기본적으로 아래 3요소가 필요하다.
  1. 전략: 실제 로직을 구현하는 객체
  2. 컨텍스트 : 전략을 사용하는 객체.
  3. 클라이언트 : 전략객체를 생성한 후 context에 주입하는 객체.

  먼저 패키지를 만들고 그 안에 '가상 총 게임'을 구현하자고 가정하면, 아래와 같은 Class가 필요할 것이다.
  ![스크린샷 2017-02-09 오후 5.53.14](http://i.imgur.com/xa4Al2w.png=100x20)

- Strategy.java
```
  public interface Strategy {
	public void runStrategy();
}
```

- Soldier.java
```
public class Soldier {
	public static final int NEAR = 0;
	public static final int FAR = 1;
	public static final int ATTACKED = 2;

	public int status = FAR;

	public void useStrategy(Strategy strategy){
		System.out.println("---전투 시작--");

		strategy.runStrategy();
		System.out.println("---전투 종료---");
	}
  ```
- StrategyGun.java
```
public class StrategyGun implements Strategy {

	@Override
	public void runStrategy() {
		System.out.println("빵야 빵야~");

	}

}
```

- StrategySword.java
```

public class StrategySword implements Strategy {

	@Override
	public void runStrategy() {
		System.out.println("찔렸당");

	}

}
```
그리고 메인에서 아래와 같이 입력하면 Strategy 디자인패턴을 조금은 이해할 수 있다.
```
    ...

    Strategy strategy = null;
		Soldier context = new Soldier();

		context.status = Soldier.NEAR;
		//전략패 전략인터페이스를 구현한 구현체를 주입한다.
		if(context.status == Soldier.ATTACKED){
			strategy = new StrategySword();
		}else if(context.status == Soldier.NEAR){
			strategy = new StrategyGun();
		}else{
			strategy = new StrategyShield();
		}

```
