### 보행자 천국

- [programmers Level3 보행자 천국](https://programmers.co.kr/learn/courses/30/lessons/1832)



### 풀이 과정

BFS를 이용했다. 조금 더 쉬운 방법으로 다시 풀어볼예정이다.



### 코드

```java
import java.util.*;
class Solution {
    int MOD = 20170805;
    public int solution(int m, int n, int[][] cityMap) {
        boolean [][] visit = new boolean[m][n];
		int [][][] count = new int [2][m][n];
		byte [] rowRoad = {0, 1};
		byte [] colRoad = {1, 0};
		LinkedList<Integer> row = new LinkedList<Integer>();
		LinkedList<Integer> col = new LinkedList<Integer>();
		LinkedList<Integer> dir = new LinkedList<Integer>();

		row.add(0);
		col.add(0);
		dir.add(0);
		visit[0][0] = true;
		count[0][0][0] = 1;
		count[1][0][0] = 0;
		int rowIndex, colIndex, direction, tempR, tempC;
		int answer = 0;
		
		while(!row.isEmpty())
		{
			rowIndex = row.remove();
			colIndex = col.remove();
			direction = dir.remove();
			if(cityMap[rowIndex][colIndex] == 2)
			{
				tempR = rowIndex + rowRoad[direction];
				tempC = colIndex + colRoad[direction];
				if(tempR < m && tempC < n && cityMap[tempR][tempC] != 1)
				{
					count[direction][tempR][tempC] = (count[direction][tempR][tempC] + count[direction][rowIndex][colIndex])%MOD;
					if(!visit[tempR][tempC] && cityMap[tempR][tempC] == 0)
					{
						visit[tempR][tempC] = true;
						row.add(tempR);
						col.add(tempC);
						dir.add(direction);
					}
					else if(cityMap[tempR][tempC] == 2)
					{
						row.add(tempR);
						col.add(tempC);
						dir.add(direction);
					}
				}
			}
			else
			{
				for(int i = 0; i < rowRoad.length; i++)
				{
					tempR = rowIndex + rowRoad[i];
					tempC = colIndex + colRoad[i];
					if(tempR < m && tempC < n && cityMap[tempR][tempC] != 1)
					{
						count[i][tempR][tempC] = (count[i][tempR][tempC] + count[0][rowIndex][colIndex] + count[1][rowIndex][colIndex])%MOD;
						if(!visit[tempR][tempC] && cityMap[tempR][tempC] == 0)
						{
							visit[tempR][tempC] = true;
							row.add(tempR);
							col.add(tempC);
							dir.add(i);
						}
						else if(cityMap[tempR][tempC] == 2)
						{
							row.add(tempR);
							col.add(tempC);
							dir.add(i);
						}
					}
				}
			}
		}
        return (count[0][m-1][n-1]+count[1][m-1][n-1])%MOD;
    }
}
```

