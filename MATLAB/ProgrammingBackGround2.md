# 2. 자료형과 변수
### 자료형
> Chapter 1에서 마지막에 했던 이야기의 정답은 '*97 또한 아스키코드상 1100001로 이해한다.*' 입니다. 그래서 a와 97을 구분하기 위해서 컴퓨터에 입력이 되는 모든 데이터에는 **자료형**(**Data Type**)이 존재합니다. 예를 들면 숫자 97은 정수이고 문자 a는 문자라는 것을 컴퓨터에게 알려줌으로써 비로소 컴퓨터는 입력이 a인지 97인지를 이해를 한다는 것입니다. 반대로 말하면, 자료형을 알려주지 않는다면 컴퓨터는 두 가지를 구분하지 못합니다. 즉, 입력이 무엇이든 간에 Default로 설정된 자료형으로 받아들입니다.
<br>
<br>
한편, 매트랩에서는 Default 자료형은 Double(실수형)이고, 따로 자료형을 선언해주지 않아도 문자와 숫자를 구분합니다. 다음의 예제를 매트랩 명령창에 입력해보세요.

```cpp
a = 97;
fprintf('%d\n',a); //출력: 97
fprintf('%c\n',a);//출력: a
```

#### 매트랩 자료형들 예시 
|Data Type|Size<sub>(Bytes)</sub>|Min|Max|Notes|
|--- |--- |--- |--- |--- |
|logical|1|0(false)|1(true)||
|int8|1|-128|+127|**Numeric, signed, integer, Exact**|
|intl6|2|-32768|+32767|**Ditto**|
|int32|4|-2147483648|+2147483647|**Ditto**|
|int64|8|-9223372036854775808|+9223372036854775807|**Ditto**|
|char|2|N/A|N/A|**Encoded Character**|
|string|varies len+1|N/A|N/A|**String of encoded characters**|

#### 숫자형 클래스 식별하기
|명령|작업|
|--- |--- |
|whos x|x의 데이터형을 표시|
|xType = class(x)|x의 데이터형을 대입|
|isnumeric(x)|x가 숫자형인지 여부를 확인|
|isa(x, 'integer')<br>isa(x, 'uint64')<br>isa(x, 'float')<br>isa(x, 'double')<br>isa(x, 'single')|x가 지정된 숫자형인지를 확인(이 표에 나온 예는 임의의 정수, 부호없는 64비트 정수, 임의의 부동소수점, 배정밀도, 단정밀도인지를 확인)|
|isreal(x)|x가 실수인지 복소수인지 확인(실수면 1, 복소수면 0을 출력)|
|isnan(x)|x가 NaN(Not-a-Number)인지를 확인|
|isinf(x)|x가 무한대인지를 확인|
|isfinite(x)|x가 유한한지를 확인|

### 변수
> 변수란 단순히 프로그램을 실행하는 동안 필요한 데이터들을 저장하기 위해 **메모리에 할당된 공간**입니다. 더 자세히는 해당 공간들을 프로그램을 실행하는 동안에만 그 프로그램 안에서 어떻게 부르겠다고 약속된 명칭입니다. 예를 들면, 벧엘관이라는 기숙사의 어떤 호실을 101호라 명명한다면 벧엘관 101호에 사는 사람은 계속 바뀔 수 있지만, 그 공간을 벧엘관101호라 부르기로 한 약속은 변하지 않았기 때문에 해당 호괸의 호실 사람들을 전부 호출하면 그 당시에 그 호관에 살고 있는 사람이 나올 것입니다.

#### 변수 선언 예시
```cpp
a = 97;
b = 98;
c = 99;
a_ch = 'a';
b_ch = 'b';
c_ch = 'c';
```
매트랩에서는 변수선언을 할 때 변수만 따로 선언할 수 없고, 반드시 선언과 함께 데이터를 같이 넣어주어야 합니다.

* [➝Chapter1 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter3 바로가기](/MATLAB/ProgrammingBackGround3.md)
* [➝Chapter4 바로가기](/MATLAB/ProgrammingBackGround4.md)
* [➝Chapter5 바로가기](/MATLAB/ProgrammingBackGround5.md)
