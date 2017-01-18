#Day8. Array, Collection, String Class

##��ü ����. 

* ��ü: ������ �ڵ�ȭ ���� ��������. ���� �ܰ迡 ����ȭ�� ������ �ڵ��ؾ� �� ���.
* Ŭ���� : ����ȭ �� ��ü�� �ڵ�ȭ ��Ų ��.
* �ν��Ͻ�(��ü): ��ü�� �޸𸮿� �ö� ��Ȳ. Ŭ������ ���ؼ� ��üX, ��üO�� �����Ѵ�.


##�迭

* 1�����迭

	int[]  array= new int[6];

* 2���� �迭

	int[][] array2 = new int[3][3];
		   	       // y,x�� �� ��.
			       //�迭 �Է�
			       //Tip : x���� ���� �����ϰ� x�� ��ȣ �տ� y�� ������ ������ �ش�.

##�ݷ���

Collection�̶� ���� Ÿ���� �������� ������ �����ϱ� ���� �ڹ� ���̺귯���̴�.

�迭�� ����ѵ� �ξ� �� ���� ����.

���� �׸��� Collection���� �ֿ� �������̽��� �������踦 ���� �ش�.

## StringŬ������ �żҵ� (���� ����ϴ�)

import java.util.Arrays;

public class Strings {

	public static void main(String[] args) {
		* 1.���ڿ� ��
		//���ڿ�.compareTo(���ڿ�)
		//���ڿ�.equals(���ڿ�)
		//���ڿ�  == ���ڿ�


		String a = "32312321";
		String b = "21223";
		String c = "1232322";

		System.out.println(a.compareTo(b));
		System.out.println(a.compareTo(c));
		
		System.out.println(a.equals(b));
		System.out.println(a.equals(c));
		
		* 2.���ڿ��� �ε��� ��
		System.out.println(a.charAt(2));
		
		* 3. ���ڿ� ��ġ��
		System.out.println(a+b);
		
		* 4. "����"���� �����ϴ� ���ڿ����� Ȯ��
		System.out.println(a.startsWith("23"));
		System.out.println(a.endsWith("22"));
		
		* 5. ã���� �ϴ� ���ڿ��� ���°���� Ȯ��
		System.out.println(a.indexOf("3"));//���ʿ� �˻��Ǵ� �ϳ��� ���� �ּҸ� �˼��ִ�. ã�� ���ڿ��� ������ -1����.
		
		* 6. ���ڿ��� ���� 
		System.out.println(a.length());
		
		* 7. ���ڿ� ����
		System.out.println(a.replace("3","x"));
		
		* 8. ���ڿ� �ڸ���
		System.out.println(a.substring(2,3)); //�ϳ��� �������ָ� 3~������.
		
		* 9. ���ڿ� �и��ϱ�
		String value = "aven/k2kj/34k2/3145";
			String values[] = value.split("/");
			for(String item : values){
				System.out.println(item);
			}
			
		* 10. ����->���ں�ȯ = ����+""
			String ccc = 888+"";
		* 11. ����->���ں�ȯ
			int ddd = Integer.parseInt(ccc); //�� ccc(888)�� ���ڿ��� ���°��� �ƴ϶� ���ڷ� ����. ��Ģ������ ����������.
			long eee = Long.parseLong(ccc);
		* 12. int -> char��ȯ = char�������� ū���� �ԷµǸ� �����.
			char fff = (char) ddd;
			
		* 13. �ϳ��� ���ڸ� char �� ���� = ����: ���ڿ����� ȿ����.
			int argNum =8;
			int argDigix = 10;
			char cha = Character.forDigit(argNum,  argDigix);
			
			String target = "8888";
			char arrs[]= target.toCharArray(); //���ڿ��� �ѱ��ھ� char�� ����.
			
		* 14. �迭 ����
		//	Arrays.sort();
	}

}
