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

지금까지 약수를 구하는 방법에 대해서 알아봤는데, 그렇다면 두 개 이상의 수가 공유하는 약수인 **공약수**와 **최대 공약수**(**Greatest Common Divisor**)를 구하기 위해서는 어떻게 구해야할까? 공약수는 최대 공약수의 약수이기 때문에 사실 최대 공약수만 알고 있다면 어렵지 않게 구할 수 있을 것이다. 하지만 최대 공약수는 단순 계산으로 구하기 힘들기 때문에 **유클리드 호제법**을 사용해서 구한다.
<br>
두 수 A와 B 사이의 최대 공약수를 gcd(A, B)로 표현할 때 A와 B는 0이 아니고 A > B라 하면, gcd(A, B) = gcd(B, A%B)와 같다. 이를 이용하여 최대 공약수를 구하는 알고리즘은 반복문과 재귀함수로 구현할 수 있다.
```cpp
//반복문으로 구현
#include <iostream>
using namespace std;

int gcd_iter(int, int);
int main()
{
	cout << gcd_iter(42, 36);
}

int gcd_iter(int a, int b)	// 항상 a > b 라고 가정
{
	int n = a % b;
	for (;;)
	{
		if (n == 0)
		{
			break;
		}

		a = b;
		b = n;
		n = a % n;
	}

	return b;
}
```
```cpp
//재귀함수로 구현
#include <iostream>
using namespace std;

int gcd_recur(int, int);

int main()
{
	cout << gcd_recur(42, 36);
}

int gcd_recur(int a, int b)	// 항상 a > b 라고 가정
{
	int n = a % b;

	if (n == 0)
	{
		return b;
	}

	else
	{
		return gcd_recur(b, a % b);
	}
}
```
### 유클리드 호제법 증명

gcd(A, B) = 
$g$라 하면 A = 
$ga$ 이고 B = 
$gb$라 할 수 있고, 이 때 
$a$와 
$b$는 서로소인 정수이다.
<br>
이 때, A를 B로 나눈 몫을 Q라하고 나머지를 R이라 하면
$ga = Qgb + R$로 표현할 수 있다.
<br>
따라서
$Qgb$를 이항하면 
$R = ga - Qgb = g(a - Qb) = gr$라고 할 수 있고, 
$B = gb$, 
$R = gr$이므로 
$g$는 B와 R사이의 공약수가 된다.
<br>
여기서 
$gcd(b,r)$이
$k$라 하면, 다시 
$b = kb'$이고
$r = kr'$ 이므로
A를 표현하면
$A = Qgb + gr = g(Qkb' + kr') = gk(Qb' + r')$ 이므로 A와 B의 최대 공약수는 
$gk$가 돼야한다. 

<br>

이는 A와 B의 최대공약수가 
$g$인 것에 대해서 모순이므로, 
$R$과 
$B$의 최대 공약수 또한 
$r$이 성립한다.
따라서 
$gcd(A, B) = gcd(B, A % B)$는 참이다.



