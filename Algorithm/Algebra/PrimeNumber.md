# 소수

### 소수
소수란 자기자신을 제외한 약수가 1밖에 존재하지 않는 수를 이야기 한다. 일반적으로 소수를 구하는 방법은 다음과 같다.
``` cpp
#include <iostream>
using namespace std;

int main()
{
	int isPrime;
  int flag = 1;
  cin >> isPrime;
	for (int i = 2; i < isPrime; i++)	//입력 받은 수의 약수가 존재하기 확인하기 위한 반복문
	{
		if(isPrime % i == 0)	//isPrime의 약수이면 true
		{
			flag = 0;
      break;
		}
	}

  if(flag){
    cout << "yes";
  }
}
```

여기서 생각해 볼만한 점은 일반적으로 나타날 수 있는 약수 중 가장 작은 약수가 2라는 것이다. 따라서 2부터 입력받은 수에 2를 나눈 값까지만 구해도 소수인지 아닌지는 판별할 수 있는 것이다. 즉 for문의 내용을 다음과 같이 바꾸어도 된다.
```cpp
  for(int i = 2; i < isPrime/2; i++){
    if(isPrime % i == 0){
      flag = 0;
      break;
    }
  }
```
하지만 2로 나눈 수도 결국 시간복잡도는 O(N)으로 같은데, 비슷한 논리로 구하고자 하는 수의 제곱근까지만 구한다면 시간복잡도를 ***O(√n)*** 으로 줄이면서 소수인지 아닌지를 판별할 수 있다. for문의 내용은 다음과 같다.
```cpp
  for(int i = 2; i*i < isPrime; i++){
    if(isPrime % i == 0){
      flag = 0;
      break;
    }
  }
```
되도록 정수로 표현을 하기 위해서 기존에 구하고자 하는 값에 루트를 씌우는 것이 아닌 i에 제곱을 하여 for문의 조건을 사용하면 기존의 시간복잡도보다 훨씬 빠르게 소수를 판별할 수 있다. 하지만 소수를 구하는 알고리즘으로 더 빠르게 구할 수 있는 방법이 존재하는데 이는 ***에라토스테네스의 체***를 이용하면 된다.

### 에라토스테네스의 체

에라토스테네스의 체는 소수를 발견하면 배열안에 존재하는 모든 수 중에서 해당 소수의 배수들을 전부 제거하는 것이다. 그림으로 표현하면 다음과 같다.
<br>
![Sieve_of_Eratosthenes_animation](https://github.com/YoungRheeCho/Today_I_Learned/assets/119858743/5b97cbb1-8284-45b8-9950-95e37d1c5ae7)
<br>
그림 출처: [에라토스테네스의 체 - 위키백과](https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4)

그림처럼 배열에 존재하는 배수들을 지워나가는 방식을 코드로 나타내면 다음과 같다.

```cpp
  int prime[100];
  int cnt = 0;
  bool check[101];
  int n = 100;
  for(int i = 2; i <= n; i++){
    if(!check[i]){
      prime[cnt] = i;
      cnt++;
      for(int j = i*i; j < n; j += i){ //단 i가 1000,000인 경우 i*i를 하면 정수범위를 넘어서므로, i*2로 하는 것이 좋다.
        check[j] = true;
      }
    }
  }
```

