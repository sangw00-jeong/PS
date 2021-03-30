### 문제

- [BOJ 1005번 Gold3 ACM Craft](https://www.acmicpc.net/problem/1005)

### 풀이 과정

지어야 하는 건물을 짓기 위해서는 건물을 지어야 하는 순서에 따라 차례로 지어야 하기 때문에 위상 정렬을 이용해 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.PriorityQueue;
import java.util.StringTokenizer;

public class Main {
    static class Structure implements Comparable<Structure>{
        private final int number;
        private final int time;

        public Structure(int number, int time) {
            this.number = number;
            this.time = time;
        }

        public int getNumber() {
            return number;
        }

        public int getTime() {
            return time;
        }

        @Override
        public int compareTo(Structure o) {
            return time - o.getTime();
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine());

        StringBuilder sb = new StringBuilder();
        int N, K, W, from, to;
        for(int i = 0; i < T; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            N = Integer.parseInt(st.nextToken());
            K = Integer.parseInt(st.nextToken());

            st = new StringTokenizer(br.readLine());
            int [] times = new int[N+1];
            int [] count = new int[N+1];
            ArrayList<Integer> [] list = new ArrayList[N+1];

            for(int j = 1; st.hasMoreTokens(); j++) {
                times[j] = Integer.parseInt(st.nextToken());
                list[j] = new ArrayList<>();
            }

            for(int j = 0; j < K; j++) {
                st = new StringTokenizer(br.readLine());
                from = Integer.parseInt(st.nextToken());
                to = Integer.parseInt(st.nextToken());

                count[to]++;
                list[from].add(to);
            }

            W = Integer.parseInt(br.readLine());

            sb.append(topologySort(times, count, list, W)).append("\n");
        }
        System.out.println(sb);

    }

    public static int topologySort(int [] times, int [] count, ArrayList<Integer>[] list, int W) {
        PriorityQueue<Structure> pq = new PriorityQueue<>();
        for(int i = 1; i < count.length; i++) {
            if(count[i] == 0) {
                pq.add(new Structure(i, times[i]));
            }
        }

        Structure cur;
        int number, time;
        while(!pq.isEmpty()) {
            cur = pq.remove();

            number = cur.getNumber();
            time = cur.getTime();

            if(number == W) {
                return time;
            }

            for(int next : list[number]) {
                if(--count[next] == 0) {
                    pq.add(new Structure(next, time + times[next]));
                }
            }
        }

        return -1;
    }
}

```

