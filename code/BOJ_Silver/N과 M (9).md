### 문제

- [BOJ 15663번 Silver2 N과 M (9)](https://www.acmicpc.net/problem/15663)

### 풀이 과정

HashSet을 이용해 중복 체크를 해서 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main {
    static ArrayList<String> list = new ArrayList<>();
    static HashSet<String> visit = new HashSet<>();
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int N = Integer.parseInt(st.nextToken());
        int M = Integer.parseInt(st.nextToken());
        int[] arr = new int[N];
        st = new StringTokenizer(br.readLine());
        for(int i = 0; st.hasMoreTokens(); i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }

        Arrays.sort(arr);
        pick(arr, new boolean[N], 0, M, "");
        print();
    }

    public static void print() {
        StringBuilder sb = new StringBuilder();
        for(String temp : list) {
            sb.append(temp).append("\n");
        }

        System.out.print(sb);
    }

    public static void pick(int[] arr, boolean[] use, int count, int M, String seq) {
        if(visit.contains(seq)) {
            return;
        }

        visit.add(seq);
        
        if(count == M) {
            list.add(seq);
            return;
        }

        for(int i = 0; i < arr.length; i++) {
            if(!use[i]) {
                use[i] = true;
                pick(arr, use, count+1, M, seq+arr[i]+" ");
                use[i] = false;
            }
        }
    }
}

```

