### 문제

- [BOJ 2533번 Gold3 사회망 서비스(SNS)](https://www.acmicpc.net/problem/2533)

### 풀이 과정

트리 dp 문제였다. 1번부터 시작해서 서브 트리의 최솟값을 더해서 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Main {
    static ArrayList<Integer>[] graph;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        graph = new ArrayList[N + 1];

        for (int i = 1; i < graph.length; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 1, n1, n2; i < N; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            n1 = Integer.parseInt(st.nextToken());
            n2 = Integer.parseInt(st.nextToken());

            graph[n1].add(n2);
            graph[n2].add(n1);
        }

        int[][] dp = new int[N + 1][2];
        for (int i = 1; i < dp.length; i++) {
            dp[i][0] = dp[i][1] = -1;
        }

        boolean[] visit = new boolean[N + 1];
        visit[1] = true;
        dfs(dp, visit, 1);

        System.out.println(Math.min(dp[1][0], dp[1][1]));
    }

    public static void dfs(int[][] dp, boolean[] visit, int n) {
        dp[n][0] = 0;
        dp[n][1] = 1;

        for(int next : graph[n]) {
            if(visit[next]) {
                continue;
            }
            visit[next] = true;
            dfs(dp, visit, next);
            dp[n][0] += dp[next][1];
            dp[n][1] += Math.min(dp[next][0], dp[next][1]);
        }
    }
}

```

