# DATA TYPE(자료형)

선언되는 모든 변수에는 자료의 형태가 존재한다.

|Data Type|Size<sub>(Bytes)</sub>|Min|Max|Notes|
|--- |--- |--- |--- |--- |
|logical|1|0(false)|1(true)||
|int8|1|-128|+127|**Numeric, signed, integer, Exact**|
|intl6|2|-32768|+32767|**Ditto**|
|int32|4|-2147483648|+2147483647|**Ditto**|
|int64|8|-9223372036854775808|+9223372036854775807|**Ditto**|
|char|2|N/A|N/A|**Encoded Character**|
|string|varies len+1|N/A|N/A|**String of encoded characters**|

### 숫자형 클래스 식별하기
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
