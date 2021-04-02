### 문제

- [BOJ 5525번 Silver2 IOIOI](https://www.acmicpc.net/problem/5525)

### 풀이 과정

주어진 문자열에서 PN을 찾았다. PN은 PN-1을 2개 만들 수 있다는 걸 이용해서 풀었다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        br.readLine();

        char [] arr = br.readLine().toCharArray();
        solve(N, arr);
    }

    public static void solve(int N, char [] arr) {
        int count = 0;
        for(int i = 0; i < arr.length-2*N;) {
            if(arr[i] != 'I') {
                i++;
                continue;
            }

            for(int j = i+1, k = 1; j < arr.length-2; j += 2, k++) {
                if(arr[j] == 'O' && arr[j+1] == 'I') {
                    if(k >= N) {
                        count++;
                    }
                    i = j+2;
                } else {
                    i = j;
                    break;
                }
            }
        }
        System.out.println(count);
    }
}

```

