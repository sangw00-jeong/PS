### 보행자 천국

- [programmers Level3 보행자 천국](https://programmers.co.kr/learn/courses/30/lessons/1832)



### 풀이 과정

BFS를 이용해 풀었지만 *풀고 나서* *dp 로만* *풀 수 있다는 걸* 알아 다시 풀었다.



### 코드

```java
import java.util.*;
class Solution {
    int MOD = 20170805;
    public int solution(int m, int n, int[][] cityMap) {
        int [][][] road = new int[2][m+1][n+1];
		
		road[0][1][1] = 1;
		road[1][1][1] = 1;
		for(int i = 1; i < road[0].length; i++)
		{
			for(int j = 1; j < road[0][i].length; j++)
			{
				if(cityMap[i-1][j-1] == 0)
				{
					road[0][i][j] += (road[0][i][j-1] + road[1][i-1][j])%MOD;
					road[1][i][j] += (road[0][i][j-1] + road[1][i-1][j])%MOD;
				}
				else if(cityMap[i-1][j-1] == 2)
				{
					road[0][i][j] = road[0][i][j-1];
					road[1][i][j] = road[1][i-1][j];
				}
			}
		}
		return (road[0][m][n-1] + road[1][m-1][n]) % MOD;
    }
}
```

