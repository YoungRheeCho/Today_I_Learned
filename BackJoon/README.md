# 백준 문제 주의사항

1. 시간초과
``` cpp
int main()
{
  // 입출력 개수가 많은 경우 아래를 추가해볼 것
  ios::sync_with_stdio(false);
  cin.tie(NULL);
  cout.tie(NULL);
}
```
2. Segmantation Fault
<br>
case 1. 비교 함수

```cpp
bool comp(int a, int b)
{
	if (a < b)
	{
		return true;
	}
  //a와 b가 같은 경우에 무조건 false를 return 해야한다.
	return false;
}
```

# Problems
* [자료구조/heap, priority queue/가운데를 말해요](/BackJoon/DataStructure/1665.md)
* [기본수학/수열](/BackJoon/Math/2575.md)
* [알고리즘/Back Tracking/스타트와 링크](/BackJoon/Algorithm/14889.md)
* [알고리즘/DP/스티커](/BackJoon/Algorithm/9465.md)
