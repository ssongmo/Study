#Day.7 �˰����� �������� ����
==================================================
## ���� : ���� �׸���

###���簢��

count�� unit�� �Է� �޾Ƽ�  1���� �����ؼ� �� ���� count�� ���ڸ�ŭ unit�� ��� �մϴ�. 

��) count =5, unit =A
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