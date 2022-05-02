# Tree 말단 노드 까지 가장 짧은 경로 DFS

사실은 시간복잡도를 위해 BFS로 하는 것이 맞다!

~~~java
import java.io.IOException;

public class Main {
    static class Node {
        int data;
        Node lt, rt;

        public Node(int val) {
            data = val;
            lt = rt = null;
        }
    }

    static Node root;
    static int level = Integer.MAX_VALUE;

    static void solution() throws IOException {
        root = new Node(1);
        root.lt = new Node(2);
        root.rt = new Node(3);
        root.lt.lt = new Node(4);
        root.lt.rt = new Node(5);
    }

    static void dfs(int L, Node root) {
        if (root == null) return;
        if (root.lt == null && root.rt == null) {
            level = Math.min(level, L);
            return;
        }
        dfs(L + 1, root.lt);
        dfs(L + 1, root.rt);
    }

    public static void main(String[] args) throws IOException {
        solution();
        dfs(0, root);
        System.out.println(level);
    }
}
~~~

