# Day11. Android Programming의 기본

##Android Runtime

* Dalvik (JIT) 기존 자바 VM과 마찬가지로 소스코드가 실행될때 한번 컴파일 , 성능 저하의 우려가 있어왔다

* ART는 설치시 최초 한번만 컴파일 하는 방식인AOT로 설계 되었으나 효율성을 위해 AOT와 JIT를 함께 사용하는 
형태로 발전하였다.

* Compile - 리눅스 상에서의 Compile 및 Build과정
* Compile : 소스코드 -> 기계어
* Link : 기계어 + 라이브러리 연결
* 안드로이드 Compile -> Dex파일을 생성
* Build : Dex파일을 apk(설치파일로 변환) ### Build Tools
* Make : 리눅스 빌드 툴 -> 소스코드를 실행파일로 만든다. (플랫폼 의존성 있음)
* Ant : 플랫폼에 독립적이면서, Java IDE의 최초 빌드툴(의존성 관리 도구가 없다.(라이브러리))
* Gradle : 안드로이드에서 사용되는 빌드 툴. 구글에서 공식 빌드로 사용하고 있기때문에 많이 사용하고 있는 추세이다.

###리눅스 빌드와 안드로이드 빌드

* 리눅스 빌드 : 컴파일(소스코드-> 기계어) + 링크(기계어+라이브러리 연결)

* 안드로이드 빌드 : 설치파일을 만들어주는 것이 빌드!

Maven : 기본 규칙(포멧)을 벗어나면 처리가 어렵다 

## Gradle

* Groovy DSL

Groovy 스타일 언어 지원 -> 컴파일 없이 스트립트 실행(Domain Specific Language 기반)

* Gradle Wrapper

Gradle Wrapper 사용으로 실제 머신에 Gradle이 업어도 빌드 가능. - Ant + Maven

별도 Gradle설치 불필요

Multi-Project 빌드가 용이함.


##Lint

Android Code Scanning Tool

문법이 이상한것들 검사하고 수정해주는 기능.

Error : 수정해야 다음으로 넘어감

Warning : 경고만 줌 (컴파일 가능)

Information : 거의 없음 (TODO)

CI(Continuous_Integration) Travis

웹상에서 빌드테스트를 하는 툴이다.



