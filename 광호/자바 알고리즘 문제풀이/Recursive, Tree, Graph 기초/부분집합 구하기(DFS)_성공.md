# 부분집합 구하기(DFS)

설명

자연수 N부터 주어지면 1부터 N까지 원소를 갖는 집합의 부분집합을 모두 출력해라



입력예제

~~~
3
~~~

출력예제

~~~
1 2 3
1 2
1 3
1
2 3
2
3
~~~



## 접근방법

~~~java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;


public class Main {

    static StringBuilder sb = new StringBuilder();
    static int N;
    static boolean[] visited;

    static void solution() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());
        visited = new boolean[N + 1];
    }

    static void dfs(int k) {
        if (k == N + 1) {
            for (int i = 1; i <= N; i++) {
                if (visited[i]) {
                    sb.append(i).append(" ");
                }
            }
            sb.append("\n");
            return;
        }

        visited[k] = true;
        dfs(k + 1);
        visited[k] = false;
        dfs(k + 1);
    }

    public static void main(String[] args) throws IOException {
        solution();
        dfs(1);
        System.out.println(sb);

    }
}
~~~

