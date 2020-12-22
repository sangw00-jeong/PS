### 2 x n 타일링

- [programmers Level3 2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)



### 풀이과정

이 문제를 푸는 방법은 처음엔 조합을 이용하여 푸는 방법을 생각해 보았다.

길이가 1, 2인 타일 2가지를 이용하여 n을 만드는 거였기에 조합을 이용하는 방법을 생각해보았다.

그렇게 하나씩 수를 대입해가며 풀어보는중 답이 피보나치 수열이라는걸 발견하게 되었다.

따라서 피보나치 수열로 푸는법이 훨씬 빠르고 편하기에 피보나치 수열로 풀었다.



### 코드

```java
class Solution {
    public int solution(int n) {
	int temp1 = 1;
	int temp2 = 2;
	int temp3 = 0;
	for(int i = 3; i <= n; i++)
	{
		temp3 = (temp1+temp2) %1000000007;
		temp1 = temp2;
		temp2 = temp3;
	}
        return temp3;
    }
}
```

