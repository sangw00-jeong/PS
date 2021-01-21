### 섬 연결하기

- [programmers Level3 섬 연결하기]()



### 풀이과정

Kruskal 알고리즘을 사용하여 풀었다.

### 코드

```java
import java.util.*;
class Solution {
    public int solution(int n, int[][] costs) {
       Arrays.sort(costs, new Comparator<int []>() {
			public int compare(int [] o1, int [] o2)
			{
				return o1[2] - o2[2];
			}
		});
		
		int [] root = new int[n];
		for(int i = 0; i < root.length; i++)
		{
			root[i] = i;
		}
		
		int sum = 0;
		int x, y;
		for(int i = 0, count = 1; count < n && i < costs.length; i++)
		{
			x = find(root, costs[i][0]);
			y = find(root, costs[i][1]);
			if(x != y)
			{
				sum += costs[i][2];
				root[y] = x;
				count++;
			}
		}
		return sum;
	}
   public static int find(int [] root, int x)
	{
		if(root[x] == x)
			return x;
		
		return root[x] = find(root, root[x]);
	}
}
```

