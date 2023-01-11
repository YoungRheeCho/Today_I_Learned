# 5. 반복문
반복문은 입력된 조건을 검사하여, 반복문으로 작성된 코드블럭 안의 내용들을 계속해서 실행하는 문장을 이야기합니다. 반복문은 크게 **for문**과 **while문**으로 나눌 수 있고 예시는 다음과 같습니다.

### 1. for문

매트랩에서는 일반적으로 알려진 언어들에서 반복문으로 사용하는 for문과는 다르게 조건을 검사하지 않고, foreach문과 흡사하게 배열에 저장된 값들을 처음부터 끝까지 하나씩 변수에 넣으며 배열 혹은 행렬에 들어있는 원소의 갯수만큼 반복문을 시행합니다. 예시는 다음과 같습니다.
```
%예제 1
for x = 1:10
    fprintf('hello\n');
end

%--------------------------
%예제 2
for x = 'hello'
    fprintf("%c",x);
end

fprintf("\n");
```
두 예제 모두 배열에 저장된 값들을 하나씩 x에 대입하며 코드블럭 안의 내용들을 반복해서 시행을 하고 있습니다. 첫 번째 예제에서는 x에 1부터 10까지 정수들을 하나씩 넣으면서 총 10번의 반복을 할 것이고 그 결과로 hello라는 문장이 총 10번이 출력됩니다. 두 번째 예제에서는 x에 'hello'라는 문자 배열이 있고 h부터 순서대로 e, l, l, o를 하나씩 입력하며 이를 출력합니다.

### 2. while문
앞에서 본 for문과는 다르게 while문에는 조건이 들어간다. 즉, while문에 입력된 조건이 참이라면 while문 안에 있는 코드들이 실행이 되고 거짓이라면 while문이 더 이상 실행되지 않고 while문 이후의 코드들이 실행될 것이다. 예시는 다음과 같습니다.
```
i = input('enter a number to repeat: ');
x = 0;

while x < i
    fprintf('hello world!');
    x = x + 1;
end
```
위 예제는 입력 받은 숫자만큼 반복문을 시행하여 hello world를 출력하는 예제입니다. x = 0부터 시작하여, 매 반복마다 x에 1을 더하고 만약 x가 i보다 작아진다면 반복문을 탈출합니다. 반복문이 돌 때 코드의 실행하는 순서는 다음과 같습니다.

![loopEx](https://user-images.githubusercontent.com/119858743/211826648-33eeaaab-8f60-4ff0-ad91-7ac03ecb43a7.PNG)

### 3. 무한 루프
while문처럼 조건을 통해 반복을 할지 말지 결정을 하는 반복문의 경우에 조건이 항상 true라면 영원히 반복을 시행하게 됩니다. 예시는 다음과 같지만 **시행하지 마시길 바랍니다.**
```
while true
    fprintf('hello world forever!\n');
end
```
이처럼 영원히 반복문을 도는 경우에는 반복문을 어떻게 제어해야 할까요? 다음 챕터에서는 반복문을 제어하는 분기문에 대해서 이야기 하겠습니다.

* [➝Chapter1 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter2 바로가기](/MATLAB/ProgrammingBackGround2.md)
* [➝Chapter3 바로가기](/MATLAB/ProgrammingBackGround3.md)
* [➝Chapter4 바로가기](/MATLAB/ProgrammingBackGround4.md)
