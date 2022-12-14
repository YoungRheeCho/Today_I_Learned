# Bubble Sort

### Bubble Sort란?

Bubble Sort의 기본적인 구조는 가장 첫번째 배열에서 시작해서 일방향으로 인접한 배열과 크기를 비교해가며 전진하는 것이다. 따라서 각 시행 마다 시작 지점과 반대 쪽 끝에는 오름차순의 경우 가장 큰 수가 위치하게 되고, 해당 배열(가장 끝 배열)을 제외한 채로 처음부터 같은 동작을 시행한다.

첫 번째 시행의 결과는 다음과 같다

| 5 | 3 | 7 | 11 | 15 | 2 | 2 | 6 | 1 | 8 |

<span style="color: #0000FF">5, 3</span>, 7, 11, 15, 2, 2, 6, 1, 8

3, 5, 7, 11, 15, 2, 2, 6, 1, 8

3, 5, 7, 11, 15, 2, 2, 6, 1, 8

3, 5, 7, 11, 15, 2, 2, 6, 1, 8

3, 5, 7, 11, 2, 15, 2, 6, 1, 8

3, 5, 7, 11, 2, 2, 15, 6, 1, 8

3, 5, 7, 11, 2, 2, 6, 15, 1, 8

3, 5, 7, 11, 2, 2, 6, 1, 15, 8

3, 5, 7, 11, 2, 2, 6, 1, 8, 15

### Bubble Sort Code 구현(c++)

```
//백준 2750번
#include <iostream> 
using namespace std;

int main() {
	int N{};
	int check = 0;

	cin >> N;
	int a[1000];
	for (int i = 0; i < N; i++) {
		cin >> a[i];
	}

	for (int i = N-1; i >=  1; i--) {
		for (int j = 0; j < i; j++) {
			if (a[j] > a[j + 1]) {
				int temp = a[j];
				a[j] = a[j + 1];
				a[j + 1] = temp;
				check = 1;
			}
		}
		if (!check) //이미 정렬이 완료되어 있을 경우에 루프를 탈출한다
			break;
		check = 0;
	}

	for (int i = 0; i < N; i++) {
		cout << a[i] << endl;
	}

}
```

### 시간복잡도

Bubble Sort의 시간 복잡도는 이미 정렬되어 있지 않은 경우를 고려하지 않는 다는 전제하에 Best Case와 Average Case 그리고 Worst case 모든 경우에 n<sup>2</sup>으로 동일하다.

