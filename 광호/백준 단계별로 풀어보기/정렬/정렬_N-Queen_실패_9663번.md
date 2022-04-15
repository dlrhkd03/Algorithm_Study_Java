# N-Queen

| 시간 제한 | 메모리 제한 | 제출  | 정답  | 맞힌 사람 | 정답 비율 |
| :-------- | :---------- | :---- | :---- | :-------- | :-------- |
| 10 초     | 128 MB      | 63268 | 31175 | 20435     | 48.617%   |

## 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

## 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

## 예제 입력 1 복사

```
8
```

## 예제 출력 1 복사

```
92
```



## 실패한 코드

~~~java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {

    static int N, cnt = 0;

    static void solution() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

    }

    static void rec_function(int k, int[][] arr) {
        if (k == N + 1) {
            cnt++;
            return;
        }
        for (int i = 1; i <= N; i++) {
            int[][] temp = arr;

            if (temp[k][i] == -1) continue;

            for (int y = 1; k + y <= N; y++) {
                temp[k + y][i] = -1;
            }
            for (int x = 1; x <= N; x++) {
                if (k + x <= N && i + x <= N) temp[k + x][i + x] = -1;
                if (k + x <= N && i - x > 0) temp[k + x][i - x] = -1;
            }
            rec_function(k + 1, temp);

        }

    }

    public static void main(String[] args) throws IOException {
        solution();
        rec_function(1, new int[N + 1][N + 1]);
        System.out.println(cnt);
    }
}
~~~

