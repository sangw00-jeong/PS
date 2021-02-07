### 문제

- [BOJ 9019번 Gold5 DSLR](https://www.acmicpc.net/problem/9019)

### 풀이 과정

너비 우선 탐색으로 풀었다. 처음 제출했을 때 시간 초과가 발생하였다. L, R 연산을 할 때 문자열로 처리하면 간단하게 코드를 작성할 수 있어서 문자열로 처리하였는데 이 부분에서 시간이 오래 걸려 시간 초과가 발생하였다. 숫자로 처리하도록 바꿔 다시 제출하였다.

### 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.StringTokenizer;

public class Main {
    static class Register {
        private int number;
        private String order;

        public Register(int number) {
            this.number = number;
            this.order = "";
        }
        public Register(int number, String order) {
            this.number = number;
            this.order = order;
        }

        public int getNumber() {
            return number;
        }

        public String getOrder() {
            return order;
        }
    }
    static char [] orders = {'D', 'S', 'L', 'R'};
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;
        int A, B;
        int T = Integer.parseInt(br.readLine());
        for(int i = 0; i < T; i++) {
            st = new StringTokenizer(br.readLine());
            A = Integer.parseInt(st.nextToken());
            B = Integer.parseInt(st.nextToken());
            BFS(A, B);
        }
    }
    public static void BFS(int A, int B) {
        LinkedList<Register> queue = new LinkedList<>();
        boolean [] visit = new boolean[10000];

        visit[A] = true;
        queue.add(new Register(A));

        Register register;
        int number, temp;
        String order;

        while(!queue.isEmpty()) {
            register = queue.removeFirst();
            number = register.getNumber();
            order = register.getOrder();

            if(number == B) {
                System.out.println(register.getOrder());
                return;
            }

            for(int i = 0; i < 4; i++) {
                temp = calculate(number, orders[i]);
                if(!visit[temp]) {
                    visit[temp] = true;
                    queue.add(new Register(temp, order+orders[i]));
                }
            }
        }
    }

    public static int calculate(int number, char order) {
        if(order == 'D') {
            number *= 2;
            number = 9999 < number ? number%10000 : number;
        } else if(order == 'S') {
            number = number == 0 ? 9999 : number-1;
        } else if(order == 'L') {
            int d1 = number/1000;
            number %= 1000;
            int d2 = number/100;
            number %= 100;
            int d3 = number/10;
            int d4 = number%10;
            number = ((d2*10 + d3)*10 + d4)*10 + d1;
        } else {
            int d1 = number/1000;
            number %= 1000;
            int d2 = number/100;
            number %= 100;
            int d3 = number/10;
            int d4 = number%10;
            number = ((d4*10 + d1)*10 + d2)*10 + d3;
        }
        return number;
    }
}

```

