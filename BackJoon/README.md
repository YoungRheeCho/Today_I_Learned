# 백준 문제 주의사항

#### 1. 시간초과

```cpp
int main()
{
	// 입출력 개수가 많은 경우 아래를 추가해볼 것
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	cout.tie(NULL);
}  
```
#### 2. Segmantation Fault / 런타임 에러 (Segfault)
* case 1. 비교 함수
```cpp
bool comp(int a, int b)
{
	if (a < b)
	{
		return true;
	}
	// a와 b가 같은 경우에 무조건 false를 return 해야한다.
	return false;
}
```

#### 3. 시간복잡도

##### 1초가 걸리는 입력의 크기
* O(1)
* O(logN)
* O(N) : 1억
* O(NlogN) : 5백만
* O(N<sup>2</sup>) : 1만
* O(N<sup>3</sup>) : 500
* O(2<sup>N</sup>) : 20
* O(N!) : 10

#### 4. EOF(End Of File)
###### c언어
```c
while(scanf("%d %d", &a, &b) == 2)
```
###### c++
```cpp
while(cin >> a >> b)
```
###### java
```c
while(sc.hasNextInt())
```

#### 5. 공백을 포함한 문자열 입력
```cpp
string str;
getline(cin,str); // 버퍼에 개행문자가 남지않음
cin >> a; //  버퍼에 개행문자가 남아있음
cin.ignore(); // 버퍼를 비움(다음 getline 함수에 개행문자가 존재하지 않도록)
cin.getline(b, 100);
cin.getline(c, 100);
```

# Problems
* [자료구조/heap, priority queue/가운데를 말해요](/BackJoon/DataStructure/1665.md)
* [기본수학/수열](/BackJoon/Math/2575.md)
* [알고리즘/Back Tracking/스타트와 링크](/BackJoon/Algorithm/14889.md)
* [알고리즘/DP/스티커](/BackJoon/Algorithm/9465.md)
