
#Day7. �˰��� ����
==================================
##���� : ���� �׸���
--------------------------------

* �⺻������ Main�� �ҷ��ͼ� �Է°��� �Է� �ް�, �� �żҵ�� ����.
### Main
-------------------------------------

	```
	public static void main(String[] args) {
		DrawPattern dp = new DrawPattern();
		dp.showRectTri(7, "X");
		dp.showReverseTri(5, "A");
		dp.showRectTri2(5, "X");
		dp.showRectTri3(7, "��");
		dp.showRectTri4(6, "��");
		dp.showDiamond(7, "A");
		dp.showDiamond2(11, "A");
	```

### ���簢��
-------------------------------------
count�� unit�� �Է� �޾Ƽ� 1���� �����ؼ� �� ���� count��  ���ڸ�ŭ unit�� ��� �մϴ�. 

 ��) count =5, unit =A
 A

 AA

 AAA

 AAAA

 AAAAA


```
	public void showRectTri(int count, String unit){
	    int i,j ;
	    for(i=1; i<=count; i++){
		    for(j=1; j<=i;j++){
			    System.out.print(unit);	
		    }
		    System.out.println("");
	    }
	}
```

### ���簢�� (������)
-------------------------------------
���簢���� �ݴ� �������� ���.
 
 ex)    
         A

        AA

       AAA

      AAAA

     AAAAA


 ```       
	public void showReverseTri(int count, String unit){
	    int i,j,k ;
	    for(i=1; i<=count; i++){
	      	//���� ���
		    for(k=count-1; k>=i; k--)
		    {
			    System.out.print(" ");
		    }
		    for(j=1; j<=i;j++){
			    System.out.print(unit);	
		    }
		    System.out.println("");
	    }
		
	}
```

### �Ƕ�̵�
-------------------------------------
�Ƕ�̵带 ���� ���.
 
 ex)    A

       AAA

      AAAAA

     AAAAAAA
  

```
	public void showRectTri2(int count, String unit){
	    int i,j,k;
	    for (i = 0; i < count; i++) {
	        for (j = 1; j < count - i; j++) {
	            System.out.print(" ");
	        }
	        for (k = 0; k < i * 2 + 1; k++) {
	            System.out.print(unit);
	        }
	        System.out.println();
	    }
	}
````


### ũ�������� Ʈ��
-------------------------------------
ũ�������� Ʈ�� ���.
  ex)    A
        A A
       A   A
      A     A

```      
	public void showRectTri3(int count, String unit){
            int i=0,j=0;
            for(i=0; i<count-1; i++){
		    for(j=i; j<count-1; j++){
			    System.out.print("  ");
		    }
	   
	            for(j=0; j<2*i+1; j++){
	       	    	if(j==0 || j==2*i)
		    		System.out.print(unit);
	    		else
	    		 	System.out.print("  ");
	       	    }
	   	    System.out.println(" ");
	    }
	}
```

### ���� �� �ﰢ��
-------------------------------------
�ؿ��� ���� �ִ� Ʈ��
 ex)    A
       A A
      A   A
     AAAAAAA

```
	public void showRectTri4(int count, String unit){
		
            int i=0,j=0,k=0;

	  
       	    for(i=0; i<count-1; i++){
		    for(j=i; j<count-1; j++){
			    System.out.print("  ");
		    }
	   
	   	    for(j=0; j<2*i+1; j++){
			    if(j==0 | j==2*i)
				    System.out.print(unit);
			    else
				    System.out.print("  ");
		    }
	   
	   	    System.out.println(" ");
	    }
	  
	    for(k=0; k<count+2; k++){
			
	    	System.out.print(unit);
	    }
	    System.out.println(" ");
	}
```

### ���̾Ƹ��
-------------------------------------
���̾Ƹ��
 ex)
         A
        AAA
       AAAAA
        AAA
         A 

```
	public void showDiamond(int count, String unit){
		int i,j,k;
		
		int middle = (count/2)+1;
		
		for (i = 0; i < middle; i++) {
		    for (j = 1; j < middle - i; j++) {
		        System.out.print(" ");
		    }
		    for (k = 0; k < i * 2 + 1; k++) {
		        System.out.print(unit);
		    }
		    System.out.println();
		}
		int minus = count;
		
		for(i= middle; i<=count; i++){
			for (j = 0; j <= i-middle; j++) {
		        System.out.print(" ");
		    }
			 for (k = minus-2; k > 0; k--) {   
				 System.out.print(unit);
			    } 
			 minus= minus -2;
		    System.out.println();
		}
		
	}
```

### �߰��� �� ���̾Ƹ��
-------------------------------------
 �߰��� ������ ���� ���̾Ƹ��

```
	public void showDiamond2(int count, String unit){
		int i,j,k;
		
		int middle = (count/2)+1;
		
		
		for (i = 0; i < middle; i++) {
		    for (j = 1; j < middle - i; j++) {
		        System.out.print(" ");
		    }
		    for (k = 0; k < i * 2 + 1; k++) {
		        if(k%2!=0){  //Ȧ���� �� ���� ���, ¦���� �� ���� ���
		    	System.out.print(unit);
		        } else{
		        System.out.print(" ");
		        }
		    }
		    System.out.println();
		}
		
		int minus = count;   //���� ������ �ٿ��ֱ� ���� ����.
		for(i= middle; i<=count; i++){
			for (j = 0; j <= i-middle; j++) { // ���� �ø���.
				
		        System.out.print(" ");
		    }
			 for (k = minus-2; k > 0; k--) { //���� ������ 2���� ����.  
				 System.out.print(unit);
			    } 
			 minus= minus -2;
		    System.out.println();
		}
		
	}
```

### ������
-------------------------------------

```
int A[][] = new int[6][6]; //1~5 ���
        int K=0; //����Ұ��� ���� ����
        int N=5; //�� ȸ������ ������ ����Ƚ���� ������ ����(5,4,3,2,1 �� �����)
        int SW=1; //(+1)��� ���� ���� , (-1)��� ���� ����
        int I=1,J=0;
       
        //[2] ó��
        do{        
            for(int P=1;P<=N;P++){ // ������ 1~5            
                K=K+1;
                J=J+SW; //����� ����ȭ
                A[I][J] = K;                               
            }          
            N=N-1;
           
            if(N>0){               
                for(int P=1;P<=N;P++){             
                    K=K+1;
                    I=I+SW; //������ �ຯȭ
                    A[I][J] = K;                               
                }              
                SW = SW*(-1); // ����Ī             
            }else{             
                break; //�ݺ��� ��������.
            }          
        }while(true);
       
       
        //[3] ���
        for(int i = 1; i<A.length;i++){        
            for(int j =1; j< A[i].length;j++){
                System.out.print(A[i][j]+"\t");                        
            }
            System.out.println();
        }      
```