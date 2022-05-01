# 최소스패닝트리 : 프림, PriorityQueue 활용



## 접근 방법

1. 인접리스트 ArrayList<ArrayList\<Edge>> list 를 사용한다.
2. PriorityQueue\<Edge>를 이용해서 가중치가 낮은 노드를 찾아낸다.
3. 모습은 BFS와 비슷한 느낌으로

~~~java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    static class Edge implements Comparable<Edge> {
        int v, cost;

        public Edge(int v, int cost) {
            this.v = v;
            this.cost = cost;
        }

        @Override
        public int compareTo(Edge e) {
            return this.cost - e.cost;
        }
    }

    static int V, E, sumCost = 0;
    static PriorityQueue<Edge> pQ = new PriorityQueue<>();
    static ArrayList<ArrayList<Edge>> graph = new ArrayList<ArrayList<Edge>>();
    static boolean[] visited;

    static void solution() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        V = Integer.parseInt(st.nextToken());
        E = Integer.parseInt(st.nextToken());
        visited = new boolean[V + 1];

        for (int i = 0; i <= V; i++) graph.add(new ArrayList<Edge>());
        for (int i = 0; i < E; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            int v1 = Integer.parseInt(st.nextToken());
            int v2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            graph.get(v1).add(new Edge(v2, cost));
            graph.get(v2).add(new Edge(v1, cost));
        }
    }

    static void prim(int v) {
        pQ.offer(new Edge(v, 0));
        int cnt = 0;
        while (!pQ.isEmpty()) {
            Edge e = pQ.poll();

            if (!visited[e.v]) {
                visited[e.v] = true;
                sumCost += e.cost;
                if (cnt++ == V) return;
                for (Edge ob : graph.get(e.v)) {
                    if (!visited[ob.v]) {
                        pQ.offer(ob);
                    }
                }
            }
        }
    }

    public static void main(String[] args) throws IOException {
        solution();
        prim(1);
        System.out.println(sumCost);
    }
}
~~~

