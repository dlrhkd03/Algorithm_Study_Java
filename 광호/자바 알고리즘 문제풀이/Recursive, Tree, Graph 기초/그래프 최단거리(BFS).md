# 그래프 최단거리(BFS)

다음 그래프에서 1번 정점에서 각 정점으로 가는 최소 이동 간선수를 출력하세요.



▣ 입력설명
 첫째 줄에는 정점의 수 N(1<=N<=20)와 간선의 수 M가 주어진다. 그 다음부터 M줄에 걸쳐 연 결정보가 주어진다.



▣ 출력설명
 1번 정점에서 각 정점으로 가는 최소 간선수를 2번 정점부터 차례대로 출력하세요.



▣ 입력예제 1

~~~
6 9
1 3
1 4 
2 1
2 5
3 4
4 5
4 6
6 2
6 5
~~~



▣ 출력예제 1 

~~~
2:3
3:1
4:1
5:2 
6:2
~~~



## 성공한 코드

~~~java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {

    static int N, M;
    static StringBuilder sb = new StringBuilder();
    static boolean[] visited;
    static int[] dis;
    static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

    static void solution() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        visited = new boolean[N+1];
        dis = new int[N+1];
        for (int i = 0; i <= N; i++) graph.add(new ArrayList<>());
        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            graph.get(a).add(b);
        }
    }

    static void bfs(int a) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(a);

        while(!q.isEmpty()) {
            int len = q.size();
            for (int i = 0; i < len; i++) {
                int cv = q.poll();
                for (int nv : graph.get(cv)) {
                    if (!visited[nv]) {
                        if (dis[nv] == 0) dis[nv] = dis[cv] + 1;
                        visited[nv] = true;
                        q.offer(nv);
                    }
                }
            }
        }
    }

    public static void main(String[] args) throws IOException {
        solution();
        visited[1] = true;
        bfs(1);
        for (int i = 1; i <= N; i++) {
            System.out.println(i + " : " + dis[i]);
        }
    }
}
~~~

