# 6. 분기문
지난 챕터에서 언급된 for문으로 작성된 이중루프를 while문으로 바꾸는 것의 답은 다음과 같습니다.
```
while i < 10
    j = 0;
    while j <= i
        fprintf('*');
        j = j + 1;
    end
    fprintf('\n');
    i = i + 1;
end
```
이번 챕터 또한 지난 챕터인 반복문의 연속인데요, 반복문을 탈출 및 제어하는 방법에 대해서 알아보려고 합니다. 우선 반복문에서 탈출하는 방법은 **break**와 **return** 두 가지가 존재합니다. 먼저 이 두 가지가 어떤 것인지, 그리고 어떻게 사용되는지 알아보겠습니다.

### 1. break
break는 프로그램의 실행을 종료하는 것이 아니라면 반복문을 탈출할 때 항상 사용되는 키워드입니다. 반복문 안에 작성된 코드블럭을 한 줄씩 읽어내려가다가 break를 만나면 그 즉시 반복문에서 나와 반복문 이 후의 코드를 실행합니다. 따라서 무한 루프에 갇혔을 때 유저로부터 입력값을 받아오는 경우처름 특정 조건에 따라 탈출할 수 있는 코드로 많이 사용됩니다. 무한 루프가 아니더라도 특정 조건에서 반복문을 탈출하고 싶을 때 사용되기도 합니다. 예시는 다음과 같습니다.

```
while true
  x = input('Enter a number: ');
  if x == 0
    fprintf("bye bye\n");
    break;
  end
  fprintf("loop\n");
end

fprintf("after loop");
```

### 2. return
return은 엄밀히 말하면 반복문을 탈출하는 것이 아니라 실행되고 있는 함수를 아예 종료하는 키워드입니다. 즉, 반복문을 탈출한 후, 이후에 나오는 코드를 실행하는 break와 달리 프로그램 자체를 종료한다고 볼 수 있으므로 당연히 반복문 이후의 모든 코드들은 실행되지 않고 종료가 됩니다. 예시는 다음과 같습니다.

```
while true
  x = input('Enter a number: ');
  if x == 0
    fprintf("bye bye\n");
    return;
  end
  fprintf("loop\n");
end

fprintf("after loop");
```
break를 사용한 예제에서 after loop라는 문자열을 출력한 것과 달리 return을 사용한 예제에서는 이를 출력하지 않고 끝난 것을 확인할 수 있을 것 입니다.
<br>
return과 break는 어쨌든 반복문을 탈출하는 방법이었는데요, 이번에는 반복문 탈출 외에도 반복문을 제어하는 키워드 중에서 반복문 안의 내용들을 실행하지 않고 바로 다음 루프를 실행할 수 있는 키워드에 대해서 이야기하겠습니다.

### 3. continue
continue는 continue 이하의 반복문을 실행하지 않고 바로 다음 루프로 넘어가는 코드인데요, 예시로 5번째 반복을 시행중에 있다가 continue코드를 만난다면 남은 코드를 실행하지 않고 바로 6번째 반복을 진행합니다. 예시는 다음과 같습니다.
```
for x = 1:10
    if mod(x,2) == 0 %mod(x,2)는 x를 2로 나누고 난 나머지
        continue
    end
    fprintf('%d ',x);
end
fprintf('\n');
```

* [➝Chapter1(프로그래밍이란?) 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter2(자료형과 변수) 바로가기](/MATLAB/ProgrammingBackGround2.md)
* [➝Chapter3(연산자) 바로가기](/MATLAB/ProgrammingBackGround3.md)
* [➝Chapter4(조건문) 바로가기](/MATLAB/ProgrammingBackGround4.md)
* [➝Chapter5(반복문) 바로가기](/MATLAB/ProgrammingBackGround5.md)
* [➝Chapter7(입출력) 바로가기](/MATLAB/ProgrammingBackGround7.md)
* [➝Chapter8(함수) 바로가기](/MATLAB/ProgrammingBackGround8.md)
