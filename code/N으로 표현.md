### N으로 표현

- [programmers Level3 N으로 표현](https://programmers.co.kr/learn/courses/30/lessons/42895)



### 풀이과정

N을 8개까지 이용하여 만들 수 있는 수를 저장할 ArrayList배열을 만들었고 N을 이용하여 만들 수 있는 수를 만들어가며 number와 비교해보았다. 만들며 나오지않았을때에는 8개로 만들 수 있는수에 number가 있을경우를 찾았고 없으면 -1을 return 한였다. 차례대로 i개를 이용하여 만든 수들과 k개를 이용하여 만들 수 있는 수와 연산을 하여 i+k개로 만들 수 있는 수를 만들었다.



### 코드

```java
import java.util.*;
class Solution {
    public int solution(int N, int number) {
		ArrayList<Integer> [] ar = new ArrayList[9];
		String s = "";
		for(int i = 1; i < ar.length; i++)
		{
			s += N;
			ar[i] = new ArrayList<Integer>();
			ar[i].add(Integer.parseInt(s));
			if(Integer.parseInt(s) == number)
			{
				return i;
			}
		}
		int max = 9;
		int temp1 = 0;
		int temp2 = 0;
		for(int i = 1; i < 8; i++)
		{
			for(int j = 0; j < ar[i].size(); j++)
			{
				temp1 = ar[i].get(j);
				for(int k = 1; k + i <= 8; k++)
				{
					for(int l = 0; l < ar[k].size(); l++)
					{
						temp2 = ar[k].get(l);
						
						if(temp1 + temp2 == number || temp1 - temp2 == number || temp1 * temp2 == number || temp1 / temp2 == number)
						{
							if(i+k < max)
								max = i+k;
						}
						
						ar[i+k].add(temp1 + temp2);
						ar[i+k].add(temp1 * temp2);
						
						if(temp1 - temp2 > 0)
							ar[i+k].add(temp1 - temp2);
						if(temp1 / temp2 > 0)
							ar[i+k].add(temp1 / temp2);
					}
				}
			}
		}
        if(max < 9)
            return max;
        else if(max == 9 && ar[8].contains(number))
            return 8;
        else
            return -1;
        
    }
}
```

