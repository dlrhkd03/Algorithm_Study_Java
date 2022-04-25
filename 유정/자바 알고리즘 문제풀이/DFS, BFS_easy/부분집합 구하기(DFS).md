# 부분집합 구하기(DFS)



자연수 N이 주어지면 1부터 N까지의 원소를 갖는 집합의 부분집합을 모두 출력하는 프로그램 을 작성하세요.

 

▣ 입력설명

첫 번째 줄에 자연수 N(1<=N<=10)이 주어집니다.

 

▣ 출력설명

첫 번째 줄부터 각 줄에 하나씩 부분집합을 아래와 출력예제와 같은 순서로 출력한다. 단 공집합은 출력하지 않습니다.

 

▣ 입력예제 1

3

 

▣ 출력예제 1

1 2 3

1 2

1 3

1

2 3

2

3



### 구현 코드

```
import java.util.*;
class Main {
	static int n;
	static int[] ch;
	public void DFS(int L){
		if(L==n+1){
			String tmp="";
			for(int i=1; i<=n; i++){
            	// 체크배열 원소 1인 것 출력
				if(ch[i]==1) tmp+=(i+" ");
			}
            // 공집합 제외
			if(tmp.length()>0) System.out.println(tmp);
		}
		else{
			ch[L]=1;  // 포함함(o)
			DFS(L+1); // 왼쪽
			ch[L]=0;  // 포함하지 않음(x)
			DFS(L+1); // 오른쪽
		}
	}

	public static void main(String[] args){
		Main T = new Main();
		n=3;
		ch=new int[n+1];
		T.DFS(1);
	}	
}
```



**문제 해설**

[Link]: https://lealea.tistory.com/75?category=1008807

