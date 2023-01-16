# 약수와 최대 공약수

### 약수
약수란 어떤 수를 나누어 떨어지게 하는 수를 말한다. 일반적으로 약수를 구하는 방법은 다음과 같다.
``` cpp
#include <iostream>
using namespace std;

int main()
{
	int N = 10;

	for (int i = 1; i < N; i++)	//10의 약수를 출력하기 위한 반복문
	{
		if(N % i == 0)	//10의 약수이면 true
		{
			cout << i << " ";
		}
	}
}
```

하지만, 이 방식은 모든 경우의 수를 탐색하므로 시간복잡도가 O(N)으로 만약 1,000,000,000개가 넘는 case가 들어오면 알고리즘 문제를 푸는 경우 시간초과로 못 푸는 경우가 생긴다. 따라서 약수를 구하는 알고리즘을 구현하기 위해서 더 빠른 시간복잡도로 풀 수 있는 효율적인 방법이 필요한데 방식은 다음과 같다.
```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
#include <iostream>
#include <cmath>
#include <vector>
using namespace std;

int main()
{
	int N = 10;
	vector<int> divisor;

	for (int i = 1; i <= sqrt(N); i++)	//10의 약수를 출력하기 위한 반복문
	{
		if (N % i == 0)	//10의 약수이면 true
		{
			divisor.push_back(i);	//배열에 약수를 입력
		}
	}
	
	int length = divisor.size();	//현재 배열의 크기
	for (int i = length - 1; i >= 0; i--)	//배열의 크기만큼 반복 시행(남은 약수의 갯수가 배열의 크기와 같거나 배열의 크기 - 1과 같기 때문)
	{
		if (N / divisor[i] != divisor[i])	//약수가 제곱근인 경우를 제외
		{
			divisor.push_back(N / divisor[i]);	// 제곱근보다 큰 약수들을 배열에 입력
			length++;	//배열에 입력할 때마다 length를 증가
		}
	}

	for (int i = 0; i < length; i++)
	{
		cout << divisor[i] << " ";	//배열을 출력
	}
}
```

약수 중 중간값은 항상 **제곱근**인 것을 이용하여 시간 복잡도를 훨씬 빠르게 한 알고리즘이다. 이 경우에 시간복잡도는 **O**(**√N**)이 되므로 10억이 들어오더라도 약 3만번 정도의 계산으로 제곱근 보다 작은 약수를 구할 수 있다. 입력받은 정수를 약수로 나눈 수 또한 약수가 되므로 마찬가지로 3만번 정도의 시행으로 제곱근 이상의 약수들을 모두 구할 수 있다.

### 유클리드 알고리즘(유클리드 호제법)


