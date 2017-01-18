#Day8. Array, Collection, String Class

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
		* 12. int -> char변환 = char범위보다 큰값이 입력되면 절삭됨.
			char fff = (char) ddd;
			
		* 13. 하나의 숫자를 char 로 변형 = 이유: 문자열보다 효율적.
			int argNum =8;
			int argDigix = 10;
			char cha = Character.forDigit(argNum,  argDigix);
			
			String target = "8888";
			char arrs[]= target.toCharArray(); //문자열을 한글자씩 char로 분해.
			
		* 14. 배열 정렬
		//	Arrays.sort();
	}

}
