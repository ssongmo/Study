#Day.7 알고리즘의 여러가지 패턴
==================================================
## 부제 : 도형 그리기

###직사각형

count와 unit을 입력 받아서  1부터 시작해서 매 라인 count의 숫자만큼 unit을 출력 합니다. 

예) count =5, unit =A
 * A
 * AA
 * AAA
* AAAA
 * AAAAA
 * 
 * @param count
 * @param unit
	 */
	public void showRectTri(int count, String unit){
		int i,j ;
		for(i=1; i<=count; i++){
			for(j=1; j<=i;j++){
				System.out.print(unit);	
			}
			System.out.println("");
		}
	}