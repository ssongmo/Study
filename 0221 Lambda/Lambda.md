## Lambda

* java 8 에 람다 표현식이 도입되면서 closure를 사용하지 않고도 함수형 언어 비슷한 코드를 작성하는게 가능해졌다. 람다 표현식은 이름이 없는 익명 함수를 의미한다. 람다 표현식을 이용함으로써 간결하고 명확한 코드로 그 의도를 표현할 수 있다.
#### 1. 람다를 사용하는 이유
* 코드량을 줄일 수 있다.
* 람다 표현식을 이용함으로써 간결하고 명확한 코드로 그 의도를 표현할 수 있다.

#### 2. 람다 사용조건
* 콜백 객체가 인자로 넘어가는 곳
* 콜백 객체에 함수가 하나여야 한다

**람다는 자바8 환경설정에서 사용해야 하기 때문에 Gradle(APP)에서 설정해줘야 한다.**
![캡처](http://i.imgur.com/acrBHQh.png)

#### 3. Syntax
```
(argument) -> (body)
```
* 콜백객체에서 하나의 함수에 있는 로직블럭만 사용된다.
* 함수명은 생략하고 괄호와 인자(타입생략)만 표시한다.
* 함수명과 로직블럭을 -> 표시로 연결한다.

```  
원형  
     public void onClick(View view){
     System.out.println(view);
     }
```

    람다 1: 함수명 생략
    - (View view) -> { System.out.println(view); }

    람다 2: 함수 인자타입 생략
    - (view) -> { System.out.println(view); }

    람다 3: 인자가 하나일 경우 함수 괄호 생략
    - view -> { System.out.println(view); }

    람다 4: 한줄일경우 코드 괄호 생략, 세미콜론 생략
    - view -> System.out.println(view)

    람다 5 : 코드측 함수가 받는 인자가 하나일 경우 참조형 메소드로 작성
            전체 생략
    - System.out::println        
