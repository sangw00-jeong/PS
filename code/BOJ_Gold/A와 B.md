### 문제

- [BOJ 12904번 Gold5 A와 B](https://www.acmicpc.net/problem/12904)

### 풀이 과정

주어진 문자열 S의 뒤에 A를 추가하거나 문자열을 뒤집어 B를 추가해 T 문자열을 만들 수 있는지 확인하는 문제다. 반대로 T 문자열의 끝이 A 면 줄이고 B 면 줄이고 방향을 바꿨다. S 문자열 길이가 될 때까지 줄여나가고 방향대로 읽어가며 S와 비교하였다.

### 코드

```java
import java.io.*;

public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    public static void main(String[] args) throws IOException {
        char[] S = br.readLine().toCharArray();
        char[] T = br.readLine().toCharArray();

        solve(S, T);
    }
    public static void solve(char[] S, char[] T) {
        if(calculate(S, T, 0, T.length-1, false)) {
            System.out.println("1");
        } else {
            System.out.println("0");
        }
    }

    public static boolean calculate(char[] S, char[] T, int start, int end, boolean dir) {
        if(end-start == S.length-1) {
            if(dir) {
                for(int i = end, j = 0; j < S.length; i--, j++) {
                    if(S[j] != T[i]) {
                        return false;
                    }
                }
            } else {
                for(int i = start, j = 0; j < S.length; i++, j++) {
                    if(S[j] != T[i]) {
                        return false;
                    }
                }
            }
            return true;
        }

        if(dir) {
            return calculate(S, T, start+1, end, T[start]=='A');
        } else {
            return calculate(S, T, start, end-1, T[end]=='B');
        }
    }
}
```

