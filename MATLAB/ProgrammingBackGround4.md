# 4. 조건문
> 조건문이란 특정 조건이 주어졌을 때 어떤 동작을 수행하도록 사용되는 문장입니다. 조건문을 사용하는 방법은 다음과 같은 방법들이 있습니다.

### if - else문
```
if true
  fprintf('true');
end
```
예시와 같이 if와 end를 통해 조건문이 실행할 동작들의 범위를 정할 수 있고, 이 안에는 if 옆에 선언되어 있는 조건에 의해 특정 조건에서만 코드 블록 안의 동작들을 수행합니다.
조건은 무조건 true 또는 false 여야 하므로 조건을 넣는 선언부에는 항상 true와 false를 출력하는 [함수]()나 조건 연산자를 통해 true 또는 false가 와야 합니다. 하지만 조건에 true나 false가 아니라 다른 숫자가 와도 기본적으로 0을 제외한 숫자는 true로 인식하기 때문에, 다음과 같은 방식으로도 조건을 설정할 수 있습니다.

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
```
* [➝Chapter1 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter2 바로가기](/MATLAB/ProgrammingBackGround2.md)
* [➝Chapter3 바로가기](/MATLAB/ProgrammingBackGround3.md)
