# Tree 말단노드까지의 가장 짧은 경로 BFS



~~~java
import java.io.IOException;
import java.util.LinkedList;
import java.util.Queue;

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
    static int L=0;

    static void solution() throws IOException {
        root = new Node(1);
        root.lt = new Node(2);
        root.rt = new Node(3);
        root.lt.lt = new Node(4);
        root.lt.rt = new Node(5);
    }

    static void bfs(Node root) {
        Queue<Node> q = new LinkedList<>();
        q.offer(root);
        L = 0;
        while (!q.isEmpty()) {
            int len = q.size();
            for (int i = 0; i < len; i++) {
                Node cur = q.poll();
                if (cur.lt == null && cur.rt == null) return;
                if (cur.lt != null) q.offer(cur.lt);
                if (cur.rt != null) q.offer(cur.rt);
            }
            L++;
        }
    }

    public static void main(String[] args) throws IOException {
        solution();
        bfs(root);
        System.out.println(L);
    }
}
~~~

