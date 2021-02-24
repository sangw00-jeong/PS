### 문제

- [BOJ 1013번 Gold5 Contact](https://www.acmicpc.net/problem/1013)

### 풀이 과정

자바의 정규식을 이용해 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.regex.Pattern;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String pattern = "(100+1+|01)+";
        int T = Integer.parseInt(br.readLine());
        for(int i = 0; i < T; i++) {
            String input = br.readLine();
            if(Pattern.matches(pattern, input)) {
                System.out.println("YES");
            } else {
                System.out.println("NO");
            }
        }
    }
}

```

