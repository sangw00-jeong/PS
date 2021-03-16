### 문제

- [BOJ 9252번 Gold5 LCS 2](https://www.acmicpc.net/problem/9252)

### 풀이 과정

Longest Common Subsequence 문제였다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        char [] s1 = br.readLine().toCharArray();
        char [] s2 = br.readLine().toCharArray();
        int [][] lcs = new int[s2.length+1][s1.length+1];

        for(int i = 0; i < s2.length; i++) {
            for(int j = 0; j < s1.length; j++) {
                if(s1[j] == s2[i]) {
                    lcs[i+1][j+1] = lcs[i][j]+1;
                } else {
                    lcs[i+1][j+1] = Math.max(lcs[i+1][j], lcs[i][j+1]);
                }
            }
        }

        int count = lcs[s2.length][s1.length];
        char [] result = new char[count];

        for(int i = s2.length, j = s1.length; 0 < count ;) {
            if(lcs[i][j-1] == count) {
                j--;
            } else if(lcs[i-1][j] == count) {
                i--;
            } else {
                result[--count] = s2[--i];
                j--;
            }
        }

        System.out.println(result.length);
        System.out.println(String.valueOf(result));
    }
}
```

