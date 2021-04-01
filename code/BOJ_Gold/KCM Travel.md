### 문제

- [BOJ 10217번 Gold1 KCM Travel](https://www.acmicpc.net/problem/10217)

### 풀이 과정

다익스트라 알고리즘을 이용했다. 비용별 시간을 2차원 배열에 저장해 최솟값을 갱신해 주었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static class Airplane implements Comparable<Airplane> {
        private final int to;
        private final int cost;
        private final int time;

        public Airplane(int to, int cost, int time) {
            this.to = to;
            this.cost = cost;
            this.time = time;
        }

        public int getTo() {
            return to;
        }

        public int getCost() {
            return cost;
        }

        public int getTime() {
            return time;
        }

        @Override
        public int compareTo(Airplane o) {
            if(time == o.getTime()) {
                return cost - o.getCost();
            }
            return time - o.getTime();
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        int N, M, K, u, v, c, d, result;
        for(int i = 0; i < T; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            M = Integer.parseInt(st.nextToken());
            K = Integer.parseInt(st.nextToken());

            ArrayList<Airplane> [] airplanes = new ArrayList[N+1];

            for(int j = 1; j < airplanes.length; j++) {
                airplanes[j] = new ArrayList<>();
            }

            for(int j = 0; j < K; j++) {
                st = new StringTokenizer(br.readLine());
                u = Integer.parseInt(st.nextToken());
                v = Integer.parseInt(st.nextToken());
                c = Integer.parseInt(st.nextToken());
                d = Integer.parseInt(st.nextToken());

                airplanes[u].add(new Airplane(v, c, d));
            }
            result = Dijkstra(airplanes, 1, N, M);

            if(result == -1) {
                sb.append("Poor KCM");
            } else {
                sb.append(result);
            }
            sb.append("\n");
        }
        System.out.println(sb);
    }

    public static int Dijkstra(ArrayList<Airplane> [] airplanes, int start, int destination, int M) {
        int [][] result = new int[M+1][airplanes.length];
        for (int[] ints : result) {
            Arrays.fill(ints, Integer.MAX_VALUE);
        }

        PriorityQueue<Airplane> pq = new PriorityQueue<>();
        pq.add(new Airplane(start, 0, 0));

        Airplane cur;
        int cost, time, nextCost, nextTime, nextTo;
        while(!pq.isEmpty()) {
            cur = pq.remove();

            start = cur.getTo();
            cost = cur.getCost();
            time = cur.getTime();

            if(start == destination) {
                return time;
            }

            if(time > result[cost][start]) {
                continue;
            }

            for(Airplane next : airplanes[start]) {
                nextCost = cost + next.getCost();
                nextTime = time + next.getTime();
                nextTo = next.getTo();
                if(nextCost <= M && nextTime < result[nextCost][nextTo]) {
                    result[nextCost][nextTo] = nextTime;
                    for(int i = nextCost+1; i <= M; i++) {
                        if(result[i][nextTo] <= nextTime) {
                            break;
                        }
                        result[i][nextTo] = nextTime;
                    }
                    pq.add(new Airplane(next.getTo(), nextCost, nextTime));
                }
            }
        }

        return -1;
    }
}

```

