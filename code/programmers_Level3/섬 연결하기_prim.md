### 섬 연결하기

- [programmers Level3 섬 연결하기]()



### 풀이 과정

Prim알고리즘을 이용하여 풀었다.



### 코드 

```java
import java.util.*;
class Solution {
    public int solution(int n, int[][] costs) {
       int [][] graph = new int[n][n];
		for(int i = 0; i < costs.length; i++)
		{
			graph[costs[i][0]][costs[i][1]] = costs[i][2];
			graph[costs[i][1]][costs[i][0]] = costs[i][2];
		}
		
		Arrays.sort(costs, new Comparator<int []>() {
			public int compare(int [] o1, int [] o2)
			{
				return o1[2] - o2[2];
			}
		});
		
		int [] bridge = new int[n];
		boolean [] visit = new boolean[n];
		Arrays.fill(bridge, Integer.MAX_VALUE);
		bridge[costs[0][0]] = 0;
		int island = costs[0][0];
		visit[island] = true;
		int count = 1;
		int min;
		int sum = 0;
		while(count < n)
		{
			min = Integer.MAX_VALUE;
			for(int i = 0; i < graph[island].length; i++)
			{
				if(!visit[i] &&graph[island][i] != 0 && graph[island][i] < bridge[i])
				{
					bridge[i] = graph[island][i];
				}
			}
			for(int i = 0; i < visit.length; i++)
			{
				if(!visit[i] && bridge[i] < min)
				{
					min = bridge[i];
					island = i;
				}
			}
			
			visit[island] = true;
			sum += min;
			count++;
		}
		return sum;
	}
}
```

