# 이진트리 순회(BFS 넓이우선탐색, 레벨탐색)



아래 그림과 같은 이진트리를 레벨탐색 연습하세요.

 



![img](https://blog.kakaocdn.net/dn/ddQuiP/btrAmyALMWj/kEaibHvIOINbPxffrrBGS0/img.png)



 

 

레벨 탐색 순회 출력 : 1 2 3 4 5 6 7



### 코드 구현

```
import java.util.*;
class Node{ 
    int data; 
    Node lt, rt; 
    public Node(int val) { 
        data=val; 
        lt=rt=null; 
    } 
} 
  
public class Main{ 
    Node root; 
    public void BFS(Node root){ 
    	// Node객체 저장하는 큐 선언
		Queue<Node> Q=new LinkedList<>();
		Q.add(root);
        // L : Level
		int L=0;
        while(!Q.isEmpty()){
            int len = Q.size();
            for(int i=0; i<len; i++){
                Node cur = Q.poll();
                // 한 레벨의 원소 출력 후 
                System.out.print(cur.data+" ");
                // 자식을 Q에 넣음, cur:현재노드, if(cur.lt!=null):말단노드 거르기 위함
                if(cur.lt!=null) Q.add(cur.lt);
                if(cur.rt!=null) Q.add(cur.rt);
            }
            // 레벨이 끝난 것이므로 ++
            L++;
            // 줄바꿈
            System.out.println();
        }
    } 
  
    public static void main(String args[]) { 
        Main tree=new Main(); 
        tree.root=new Node(1); 
        tree.root.lt=new Node(2); 
        tree.root.rt=new Node(3); 
        tree.root.lt.lt=new Node(4); 
        tree.root.lt.rt=new Node(5); 
    	tree.root.rt.lt=new Node(6); 
        tree.root.rt.rt=new Node(7);
        tree.BFS(tree.root); 
    } 
}
```



**문제 해설**

[Link]: https://lealea.tistory.com/76?category=1008807

