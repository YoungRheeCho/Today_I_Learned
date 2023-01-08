# 4. 조건문
> 조건문이란 특정 조건이 주어졌을 때 어떤 동작을 수행하도록 사용되는 문장입니다. 조건문을 사용하는 방법은 다음과 같은 방법들이 있습니다.

### 1. if - else문
```
if true
  fprintf('true');
end
```
예시와 같이 if와 end를 통해 조건문이 실행할 동작들의 범위를 정할 수 있고, 이 안에는 if 옆에 선언되어 있는 조건에 의해 특정 조건에서만 코드 블록 안의 동작들을 수행합니다.
조건은 무조건 true 또는 false 여야 하므로 조건을 넣는 선언부에는 항상 true와 false를 출력하는 [함수]()나 조건 연산자를 통해 true 또는 false가 와야 합니다. 하지만 조건에 true나 false가 아니라 다른 숫자가 와도 기본적으로 0을 제외한 숫자는 true로 인식하기 때문에, 다음과 같은 방식으로도 조건을 설정할 수 있습니다.

##### if 예시
```
if 1  %true
  fprintf('hello world');
end

if -1 %true
  fprintf('hello world');
end

if 0.1 %true
  fprintf('hello world');
end

a = 1;
if a  %true
  fprintf('hello world');
end

if 0  %false
  fprintf('hello world');
end

if ~false %true
  fprintf('hello world');
end

if ~true %false
  fprintf('hello world');
end
```

##### else if 예시
```
input x = 'enter a number: ';

% 항상 if 출력
if x > 1
  fprintf('if\n');
elseif x > 3
  fprintf('else if\n');
end

%조건에 따라 출력
if x > 1
  fprintf('if\n');
elseif x < 0
  fprintf('else if\n');
end


if x > 1
  fprintf('if\n');
elseif x < 0
  fprintf('else if\n');
end
```
else if는 if문의 조건이 false가 되었을 때 다음으로 조건을 확인하는 구문입니다. 따라서 if가 true이면 else if문은 보지도 않고 건너뛰는 것이죠. 이 때문에 첫번째 예제처럼 조건문이 작성되었다면 그건 아마도 잘못된 조건문일 것입니다.

##### else 예시
```
input x = 'enter a number: ';

if x > 10
  fprintf('if\n');
elseif x < 0
  fprintf('else if\n');
else
  fprintf('else\n');
end
```
else는 if와 else if 모두 적용되지 않을 때, 실행되는 코드블럭입니다. 무조건 조건문에 따라서 반드시 하나는 실행되어야 한다면, else를 써야만 입력값의 모든 범위를 커버할 수 있습니다.

### 2. 중첩 if문
조건문 안에 조건문을 사용하면 어떻게 될까요? 조건문 안에서 다시 한번 조건 판단하는 동작이 실행될 것입니다. 간단히는 논리연산자를 사용하여 조건을 중첩시킬 수 있는 것을 저번 챕터에서 확인했습니다. 하지만 조건이 많이 세분화가 되는 경우에는 조건문을 중첩해서 사용하는 것이 편할 때가 많습니다. 중첩 조건문의 예시는 다음과 같습니다.

```
x = 1;

if isnumeric(x)
  if x > 0
    fprintf('positive\n');
  elseif x < 0
    fprintf('negative\n');
  else
    fprintf('zero\n');
  end
else
  fprintf('string');
end
```
* [➝Chapter1 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter2 바로가기](/MATLAB/ProgrammingBackGround2.md)
* [➝Chapter3 바로가기](/MATLAB/ProgrammingBackGround3.md)
