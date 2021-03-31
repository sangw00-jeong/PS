### 문제

- [BOJ 2098번 Gold1 외판원 순회](https://www.acmicpc.net/problem/2098)

### 풀이 과정

비트 마스킹을 하여 visit을 확인했다. BFS로 탐색을 하였는데 내일 DFS로 다시 풀어봐야겠다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.StringTokenizer;

public class Main {
    static class City {
        private final int number;
        private final int visit;

        public City(int number, int visit) {
            this.number = number;
            this.visit = visit;
        }

        public int getNumber() {
            return number;
        }

        public int getVisit() {
            return visit;
        }
    }
    static int [][] graph;
    static int [][] cost;
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        graph = new int[N][N];
        cost = new int[N][1<<N];

        for(int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int j = 0; st.hasMoreTokens(); j++) {
                graph[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        solve();
    }
    public static void solve() {
        int end = (1 << graph.length)-1;
        System.out.println(BFS(0, end));
    }

    public static int BFS(int start, int end) {
        LinkedList<City> cities = new LinkedList<>();
        cities.add(new City(start, 1 << start));

        City cur;
        int number, visit, next, min = Integer.MAX_VALUE;
        while(!cities.isEmpty()) {
            cur = cities.removeFirst();

            number = cur.getNumber();
            visit = cur.getVisit();

            if(visit == end) {
                if(graph[number][start] != 0) {
                    min = Math.min(min, cost[number][visit]+graph[number][start]);
                }
                continue;
            }

            for(int i = 0; i < graph.length; i++) {
                next = visit | 1 << i;
                if(graph[number][i] != 0 && visit != next && (cost[i][next] == 0 || cost[number][visit] + graph[number][i] < cost[i][next])) {
                    cost[i][next] = cost[number][visit] + graph[number][i];
                    cities.add(new City(i, next));
                }
            }
        }
        return min;
    }
}

```

