# Counting Sort

> ### Countig Sort란?
주어진 배열의 값 범위를 알고 있을 때, 실용적인 정렬방식으로 최댓값과 입력 배열의 원소 값 개수를 누적합으로 구성한 배열로 정렬을 수행한다. Counting Sort의 시행결과는 다음과 같다.



**처음배열:**
|3|1|2|2|4|5|
|--- |--- |--- |--- |--- |--- |

**Max Value: 5**

**Counting Array: 배열의 각 index에 각 숫자의 빈도 수를 입력한 후에 누적합 배열로 바꿔준다.**
|0|1|2|1|1|1|
|--- |--- |--- |--- |--- |--- |

**Counting Array_re:**
|c1|c2|c3|c4|c5|c6|
|--- |--- |--- |--- |--- |--- |
|0|1|3|4|5|6|

**Result:**
|b1|b2|b3|b4|b5|b6|
|--- |--- |--- |--- |--- |--- |

+ c1 = 1 : b1에 할당
+ c2 = 2 : b2부터 b3까지 할당
+ c3 = 1 : b4에 할당
+ c4 = 1 : b5에 할당
+ c5 = 1 : b6에 할당

이 과정에 따라 배열이 할당되는 과정은 다음과 같다
![counting sort](https://user-images.githubusercontent.com/119858743/209636019-9ca78209-a4f3-4f93-a349-c85c8345ac29.png)

> ### Counting Sort 코드구현(c++)
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
	int N{};
	int c[10001]{};
	int max{};
	vector<int> arr;
	vector<int>Result;
	

	cin >> N;
	//Result.reserve(N);
	Result.assign(N, 0);

	for (int i = 0; i < N; i++)
	{
		int input;
		cin >> input;
		if (input > max)
			max = input;

		c[input]++;
		arr.push_back(input);
	}

	for (int i = 1; i <= max; i++)
	{
		c[i] += c[i - 1];
	}

	for (int i = 0; i < N; i++)
	{	
		Result[c[arr[i]]-1] = arr[i];
		c[arr[i]]--;
		cout << "check";
	}

	for (int i = 0; i < N; i++)
	{
		cout << Result[i];
	}
}

```

```cpp
//백준 10989
#include <iostream>
using namespace std;

int main() {
	ios::sync_with_stdio(false);
	cin.tie(NULL);

	int N{};
	int c[10001]{};
	int max{};
	

	cin >> N;

	for (int i = 0; i < N; i++)
	{
		int input;
		cin >> input;

		c[input]++;
	}

	for (int i = 0; i < 10001; i++)
	{	
		if (c[i]) {
			for (int j = c[i]; j > 0; j--)
			{
				printf("%d\n", i);
			}
		}
	}
}

```
