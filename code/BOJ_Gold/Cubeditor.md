### 문제

- [BOJ 1701번 Gold2 Cubeditor](https://www.acmicpc.net/problem/1701)

### 풀이 과정

두 번 이상 나오는 부분 문자열 중에서 가장 긴 부분 문자열을 찾는 문제이다. 두 번 이상 나오는 부분 문자열은 접두사와 접미사가 같은 문자열이다. 전체 부분 문자열의 접두사와 접미사를 비교해 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char [] arr = br.readLine().toCharArray();
        System.out.println(solve(arr));
    }

    public static int solve(char [] arr) {
        int max = 0;
        for(int i = 0; i < arr.length; i++) {
            int [] pi = new int[arr.length];
            for(int j = i+1, k = i; j < arr.length; j++) {
                while(k > i && arr[j] != arr[k]) {
                    k = pi[k-1]+i;
                }

                if(arr[j] == arr[k]) {
                    pi[j] = ++k-i;
                    max = Math.max(max, pi[j]);
                }
            }
        }

        return max;
    }
}

```

