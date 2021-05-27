### 문제

- [BOJ 17404번 Gold4 RGB거리 2](https://www.acmicpc.net/problem/17404)

### 풀이 과정

i 번째 집을 빨강으로 칠하는 경우 최솟값은 i-1 번째 집에 초록으로 칠하는 최솟값 + i 번째 집에 빨강을 칠하는 비용과 i-1 번째 집에 파랑을 칠하는 최솟값 + i 번째 집에 빨강을 칠하는 비용 중에 작은 값이 최솟값이다. 1번 집과 N 번 집에 색이 같으면 안 된다는 조건이 있기 때문에 2번 집에 더할 1번 집의 최솟값을 고정시켜서 구했다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static int color = 3;
    public static void main(String[] args) throws IOException{
        int N = Integer.parseInt(br.readLine());
        int[][] cost = initCost(N);

        solve(cost, N);
    }

    public static void solve(int[][] cost, int N) {
        int[][] dp = new int[color][N];

        int min = 999999;
        for(int i = 0; i < color; i++) {
            for(int j = 0; j < color; j++) {
                if(i == j) {
                    dp[j][1] = 999999;
                } else {
                    dp[j][1] = cost[0][i] + cost[1][j];
                }
            }

            for(int j = 2; j < N; j++) {
                dp[0][j] = Math.min(dp[1][j-1], dp[2][j-1]) + cost[j][0];
                dp[1][j] = Math.min(dp[0][j-1], dp[2][j-1]) + cost[j][1];
                dp[2][j] = Math.min(dp[0][j-1], dp[1][j-1]) + cost[j][2];
            }

            for(int j = 0; j < color; j++) {
                if(i == j) {
                    continue;
                }
                min = Math.min(min, dp[j][N-1]);
            }
        }

        System.out.println(min);
    }

    public static int[][] initCost(int N) throws IOException {
        int[][] cost = new int[N][color];
        for(int i = 0; i < cost.length; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int j = 0; st.hasMoreTokens(); j++) {
                cost[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        return cost;
    }
}

```

