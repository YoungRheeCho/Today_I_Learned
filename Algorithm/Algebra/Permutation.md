# 순열

순열이란 어떠한 수열을 나열하는 방법들을 이야기하며, N개의 수를 나열하여 수열을 만드는 방법의 가짓 수는 N!이다. 
### 다음 순열 - Next Permutation
```1, 2, 3```이라는 수를 가진 수열을 나열하는 방법의 가짓 수는 총 6가지로 모든 순열을 구하면 다음과 같다.
```
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```
이 때, 각 순열의 수열들을 사전순으로 나열을 한다면 어떠한 순열의 다음에 오는 수열과 이전에 왔던 수열을 알 수가 있다. 이에 대한 시간 복잡도는 **O**(**N**)이고, C++의 경우 이를 구하는 함수가 ```algorithm``` 헤더에 **next_permutation**과 **pre_permutation**로 이미 존재한다. 다음 순열을 구하기 위한 조건은 다음과 같다.
* A[i-1] < A[i]를 만족하는 가장 큰 i를 찾는다.
* j >= i 이면서 A[j] > A[i - 1]를 만족하는 가장 큰 j를 찾는다.
* A[i- 1]과 A[j]를 swap한다.
* A[i]부터 순열을 뒤집는다.

  위와 같은 논리를 그림으로 나타내면 다음과 같다.
![1](https://github.com/YoungRheeCho/Today_I_Learned/assets/119858743/7c529b7b-8fb4-44ea-a59f-1b7e88eb2f63)
![2](https://github.com/YoungRheeCho/Today_I_Learned/assets/119858743/4e0765f8-cc7a-4153-975b-1bf77120b55e)
![3](https://github.com/YoungRheeCho/Today_I_Learned/assets/119858743/d6dc319e-0614-4f71-bca0-2bbff081f9b0)

이렇게 되는 이유는 수열의 끝부분부터 오름차순이 끝나는 지점은 어떤 순열의 마지막 부분이라 할 수 있다. 그리고 다음 순열은 어떤 순열의 시작 부분이 된다. 즉, 예시에서는 **512430**은 **512로 시작하는 순열의 마지막 수열**이고 그 다음 순열인 **513024**는 앞부분이 **513으로 시작하는 순열의 시작하는 수열**이다. 첫 번째 조건은 해당 순열이 어떤 순열의 마지막 순열인지를 찾는 것이고, 두 번째 조건은 그 다음으로 와야하는 순열을 찾는 것이며, 마지막 조건은 내림차순을 오름차순으로 바꿔줌으로써 시작하는 순열로 바꾸어준 것이다. 시간복잡도가 **O**(**N**)인 이유는 **첫 조건에서 역순으로 볼 때 오름차순이 끝나는 구간을 찾기 위해서 드는 복잡도 N**과 **두 번째 조건에서 기준점과 swap을 하기 위해 j를 찾기 위해서 드는 복잡도 N**을 더하여 총 **2N**이기 때문이다. algorithm에 내장된 함수를 사용한다면 다음과 같고



``` cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main()
{
	vector<int> a;
  a.push_back(5);
  a.push_back(1);
  a.push_back(2);
  a.push_back(4);
  a.push_back(3);
  a.push_back(0);

  next_permutation(a.begin(), a.end());
  for(int i : a){
    cout << i;
  }
}
```

다음 순열을 구하는 코드를 직접 만든다면 다음과 같다.
```cpp
#include <iostream>
#include <vector>
using namespace std;

void next_permutation(vector<int> &);
int main() {
  vector<int> a;
  a.push_back(5);
  a.push_back(1);
  a.push_back(2);
  a.push_back(4);
  a.push_back(3);
  a.push_back(0);

  next_permutation(a);
  for (int i : a) {
    cout << i;
  }
}

void next_permutation(vector<int> &a) {
  int size = a.size();
  for (int i = size - 1; i >= 0; i--) {
    if (i == 0) {
      cout << "end of permutation";
      break;
    }

    if (a[i] > a[i - 1]) {
      for (int j = size - 1; j >= i; j--) {
        if (a[j] > a[i - 1]) {
          int temp = a[j];
          a[j] = a[i - 1];
          a[i - 1] = temp;
          break;
        }
      }

      int index = i;
      for (int k = size - 1; k > index; k--, index++) {
        int temp = a[k];
        a[k] = a[index];
        a[index] = temp;
      }

      break;
    }
  }
}
```





