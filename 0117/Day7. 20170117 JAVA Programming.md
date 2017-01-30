
#Day7. 알고리즘 패턴
==================================
##부제 : 도형 그리기
--------------------------------

* 기본적으로 Main에 불러와서 입력값을 입력 받고, 각 매소드로 구현.
### Main
-------------------------------------

	```
	public static void main(String[] args) {
		DrawPattern dp = new DrawPattern();
		dp.showRectTri(7, "X");
		dp.showReverseTri(5, "A");
		dp.showRectTri2(5, "X");
		dp.showRectTri3(7, "☆");
		dp.showRectTri4(6, "★");
		dp.showDiamond(7, "A");
		dp.showDiamond2(11, "A");
	```

### 직사각형
-------------------------------------
count와 unit을 입력 받아서 1부터 시작해서 매 라인 count의  숫자만큼 unit을 출력 합니다. 

 예) count =5, unit =A
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

### 직사각형 (역방향)
-------------------------------------
직사각형을 반대 반향으로 출력.
 
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
	      	//공백 출력
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

### 피라미드
-------------------------------------
피라미드를 만들어서 출력.
 
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


### 크리스마스 트리
-------------------------------------
크리스마스 트리 출력.
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

### 속이 빈 삼각형
-------------------------------------
밑에가 막혀 있는 트리
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

### 다이아몬드
-------------------------------------
다이아몬드
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

### 중간이 빈 다이아몬드
-------------------------------------
 중간에 공백을 넣은 다이아몬드

```
	public void showDiamond2(int count, String unit){
		int i,j,k;
		
		int middle = (count/2)+1;
		
		
		for (i = 0; i < middle; i++) {
		    for (j = 1; j < middle - i; j++) {
		        System.out.print(" ");
		    }
		    for (k = 0; k < i * 2 + 1; k++) {
		        if(k%2!=0){  //홀수일 때 글자 출력, 짝수일 땐 공백 출력
		    	System.out.print(unit);
		        } else{
		        System.out.print(" ");
		        }
		    }
		    System.out.println();
		}
		
		int minus = count;   //별의 갯수를 줄여주기 위한 변수.
		for(i= middle; i<=count; i++){
			for (j = 0; j <= i-middle; j++) { // 공백 늘리기.
				
		        System.out.print(" ");
		    }
			 for (k = minus-2; k > 0; k--) { //별의 갯수를 2개씩 감소.  
				 System.out.print(unit);
			    } 
			 minus= minus -2;
		    System.out.println();
		}
		
	}
```

### 달팽이
-------------------------------------

```
int A[][] = new int[6][6]; //1~5 사용
        int K=0; //출력할값을 담은 변수
        int N=5; //각 회전에서 수행할 수행횟수가 지정될 변수(5,4,3,2,1 로 변경됨)
        int SW=1; //(+1)행과 열의 증가 , (-1)행과 열의 감소
        int I=1,J=0;
       
        //[2] 처리
        do{        
            for(int P=1;P<=N;P++){ // 시작은 1~5            
                K=K+1;
                J=J+SW; //행고정 열변화
                A[I][J] = K;                               
            }          
            N=N-1;
           
            if(N>0){               
                for(int P=1;P<=N;P++){             
                    K=K+1;
                    I=I+SW; //열고정 행변화
                    A[I][J] = K;                               
                }              
                SW = SW*(-1); // 스위칭             
            }else{             
                break; //반복문 빠져나감.
            }          
        }while(true);
       
       
        //[3] 출력
        for(int i = 1; i<A.length;i++){        
            for(int j =1; j< A[i].length;j++){
                System.out.print(A[i][j]+"\t");                        
            }
            System.out.println();
        }      
```