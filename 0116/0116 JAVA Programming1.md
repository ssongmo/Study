## Day6. Java Programming (Basic Syntax)
===========================================================

###�ڹ��� ������ �����?

JAVA�� 2�������� �������� ����ȴ�. VM.. (�ڼ��ϰ� �˾ƺ���)

* ������ ����

  * JIT(Just In Time) - ���� �� ���� �ѹ� ����� ������, ���� �ѹ��� �ӵ� ���ϰ� �� ���� �ִ�. (��ġ�ϰ� ���������� �������Ѵ�.)
  * AOT(Ahead Of Time) - class ������ ��ġ�� ���� �ѹ� ����� �������� �Ѵ�. 
                     �ӵ� ���ϴ� ������ �ȵ���̵� ó�� ��ġ�� ��Ȯ�� ���������� ����.
  * ART - ���� ��ģ ���. �ֱٿ� ���ԵǾ���.

  * final - �������� ���̻� �������� ���ϰ� �� ��.
  *string�� �⺻ �ڷ����� �ɼ� ����.

##0. ���� Ŭ���� ����.
-----------------------------------------------
   * ���� Ŭ������ �ݵ�� �����ؾ��ϸ� �̰����� �żҵ带 �ҷ��鿩 ����Ѵ�.

```

public class HelloWorld {  //HelloWorld��� Ŭ������ ����.

	public static void main(String[] args) { //���� �żҵ带 ����. �ڷ��� : String�迭.
		
		HelloWorld hello = new HelloWorld(); //����. (HelloWorld�ڷ����� ���� hello�� new(���ο�)�Լ��� ����.)
	}
}  //��� �ڵ��� �� Ŭ���� �ȿ����� ���� �Ǿ�� �Ѵ�.

```
##1. ������
-------------------------------------------------
* ���� �ֿܼ� ����ϴ� �Լ�.

```
public void print(int value) {
		System.out.println(value);
	}
```

*���ϱ� ( ���� ��Ģ������ ��� ������ ����.)

```
public int sum(int a, int b) {
		int result = 0;
		result = a+b;
		
		return result;
	}
```

##2. ���ǹ�
--------------------------------------------------
* if��
   
    �� ����� ������ ���������� �Ǵ��Ͽ� �ش� �� ���� �ִ� ������ �����Ѵ�.

```
public void condition(){
		int a = 15;
		int b = 20;
		int c = 15;
		
		if(a>b){
			System.out.println("a�� b���� Ů�ϴ�.");
		} else if(a == b){
			System.out.println("a�� b�� �����ϴ�.");
		}else{
			System.out.println("a��b���� �۽��ϴ�.");
		}
		
		//3�� ������
		c = (a==15)? 100:0; // a�� 15�� ���� 100�� ��� �ƴϸ� 0�� ���.
```
	
* switch��

    �Էµ� ���� � Ư������ ���Ͽ� �ش� �� ���� �ִ� ������ �����Ѵ�.

```

switch(a){
			case 1 :
				System.out.println("a�� 1�Դϴ�.");
				break;
			case 15 :
				System.out.println("a�� 15�Դϴ�.");
				break;
			case 20 :
				System.out.println("a�� 20�Դϴ�.");
				break;
			default :
				System.out.println("a�� "+ a +"�Դϴ�.");
				break;
			
		}	

```

##3.�ݺ���
------------------------------------------------------
* for��
    
   Ư�� �������� ����ŭ �ݺ��ϸ鼭 ������ ������ �����Ѵ�.

```
for(int i=0; i<10; i++){ // i����, ����, ���� (�Լ��� ���� ������ ����, ������ ����Ȯ��. �� 1,3,2
			System.out.println("i=" + i);
		}
```
	
* while��
    
   Ư�� ������ ������ �� ������ ������ �����Ѵ�.


```

while(i<limit){
			System.out.println("i2" + i);
			i = i+1;
		}

```

+�߰� ���.  

   * break; : ���ǹ��� ������ �����Ҷ������� ȸ���ϰ� �żҵ带 �������´�.
    
   * continue; : ���ǹ��� �����ϸ� �� �̻� �ݺ����� �������� �ʴ´�.


##���� ����
========================================================

###1. ������ 

* ���� for���� �̿�.

```
main �Լ��� hello.gugudan(int dan);
```

```
public int gugudan(int dan){
		int i,j;	//�ݺ���
		int result =0; //����� �ʱ�ȭ
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

###2. �Ž����� ��� ( �Ž����� ����+���� ���� ���ϱ�)


* main �Լ�

```
hello.calculate(10000, 3720); //�Է°�, ������ ��.
```

*calculate(int x, int y)�Լ�

```
public void calculate(int payed, int amount){
		int remainder;//�Ž�����
		
		int bill_5000=0;
		int bill_1000=0;
		int coin_500=0;
		int coin_100=0;
		int coin_50=0;
		int coin_10=0;
		
		remainder = payed - amount;
		System.out.println("�ܵ� :"+ remainder+"��");
		
		bill_5000 = remainder/5000; //��õ�� �ܵ� ���� Ȯ��
		remainder = remainder - (5000 * bill_5000);// �ܵ� - ��õ����
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
		
		System.out.println("��õ�� "+bill_5000+"��");
		System.out.println("õ�� "+bill_1000+"��");
		System.out.println("����� "+coin_500+"��");
		System.out.println("��� "+coin_100+"��");
		System.out.println("���ʿ� "+coin_50+"��");
		System.out.println("�ʿ� "+coin_10+"��");
	}

```

3. int������ ū ������ �Է¹��� ������ ��� ���ϱ�. (���콺 ���� �̿�)


* main �Լ�

```
//hello.sum();
``` 

* sum �Լ�

```
public long sum(){
		//1���� 3,333,333,333���� ���ϴ� �Լ��� ����� ��� ���� ���� �޾Ƽ� ����ϼ���.
		long i=0;
		long limit = 3333333333l;
		long sum = (i+limit)*((limit+1)/2);   //���콺 ���� : (1+n)*n/2
		//long sum = (i+limit)*limit/2;
		/*
		long sum = 0;
		for(i=0; i<limit+1; i++){
			sum= sum + i;
		}*/
		System.out.println("��: " + sum);
		return sum;
	
	}
```
