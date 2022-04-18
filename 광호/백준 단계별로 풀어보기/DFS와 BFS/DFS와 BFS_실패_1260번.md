# DFS와 BFS

| 시간 제한 | 메모리 제한 | 제출   | 정답  | 맞힌 사람 | 정답 비율 |
| :-------- | :---------- | :----- | :---- | :-------- | :-------- |
| 2 초      | 128 MB      | 176946 | 63501 | 37513     | 35.090%   |

## 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

## 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

## 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

## 예제 입력 1 복사

```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

## 예제 출력 1 복사

```
1 2 4 3
1 2 3 4
```



## 접근 방법

* 인접행렬로 구현한 방식
  * 꼭지점의 갯수가 적을 때 사용하는 방법

~~~java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {

    static int N, M, V;
    static int[][] map;
    static boolean[] visit;
    static StringBuilder sb = new StringBuilder();

    static void solution() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        V = Integer.parseInt(st.nextToken());
        map = new int[N + 1][N + 1];
        visit = new boolean[N + 1];

        for (int i = 0; i < M; i++) {
            String edge = br.readLine();
            st = new StringTokenizer(edge, " ");
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            map[a][b] = 1;
            map[b][a] = 1;
        }
    }

    static void dfs(int v) {
        visit[v] = true;
        sb.append(v).append(" ");

        for (int i = 1; i <= N; i++) {
            if (!visit[i] && map[v][i] == 1) {
                dfs(i);
            }
        }
    }

    static void bfs(int v) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(v);
        visit[v] = true;
        while (!q.isEmpty()) {
            int temp = q.poll();
            sb.append(temp).append(" ");

            for (int i = 1; i <= N; i++) {
                if (!visit[i] && map[temp][i] == 1) {
                    q.offer(i);
                    visit[i] = true;
                }
            }
        }
    }

    public static void main(String[] args) throws IOException {
        solution();
        dfs(V);
        sb.append("\n");
        Arrays.fill(visit, false);
        bfs(V);
        System.out.println(sb);
    }
}
~~~

