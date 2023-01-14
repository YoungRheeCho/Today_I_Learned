# 8.함수

> 함수란 특별한 목적의 작업을 수행하기 위해 만들어진 코드블럭입니다. 보통 특정 작업을 여러 번 수행하는 경우에 그 작업이 필요할 때마다 함수를 호출해서 작업을 지시함으로써 코드의 가독성을 올리기 위해 사용되며, 크게 **메인함수**와 **사용자 정의 함수**로 나뉩니다. 매트랩에서 함수 선언의 예시를 보고 설명을 마저 하겠습니다. 사용자 정의 함수를 선언하는 방법은 다음과 같습니다.
<br>

![함수](https://user-images.githubusercontent.com/119858743/212459751-3e9bdb35-53dd-4225-a45b-1e595ebb4983.PNG)

```
function sub = subEX(a, b)
    if a > b
        sub = a - b;
        return;
    elseif b > a
        sub = b - a;
        return;
    end
    sub = 0;
end
```

위의 예시에서 function과 end는 조건문이나 반복문처럼 function을 수행할 코드블럭의 선언부와 끝을 의미합니다. 즉 function 부분부터 시작해서 end까지 코드를 하나씩 실행하겠다는 것을 의미합니다. *또한 대입연산자의 좌항인 sub은 **함수가 끝나면 반환**을 할 값입니다.* 마지막으로 대입연산자의 우항에는 **함수의 이름**이 나오고 괄호 안에는 **매개변수**를 입력합니다. 매개변수는 일반적으로 수학에서 사용하는 f(x)에서 정의역(x)과 같다고 생각할 수 있습니다. 즉, 함수를 실행할 때 처리할 input값이며 반환값은 처리 후 함수의 output입니다.
<br>
한편 반복문에서도 이야기 했듯이 return은 실행 중이던 함수를 종료하고 반환값을 반환하는 명령어입니다. 따라서 예제에서는 각 조건에 따라 return을 하도록 되어있고 조건에 맞지 않는 다면 0을 return 하도록 되어있습니다.

<br>
이제 사용자 정의 함수에 대해서는 어느정도 감이 오실거라고 생각합니다. 그렇다면 main함수란 무엇일까요? 매트랩에서는 다른 언어들과 다르게 따로 main함수를 선언하지 않기 때문에 이 개념이 약간은 혼란이 올 수도 있습니다. 기본적으로 프로그래밍에서는 main함수라는 가장 큰 틀의 함수가 돌고 그 안에서 사용자 정의 함수같은 subfunction들이 돌아갑니다.
이해를 돕기 위해 수학적으로 표현을 한다면, 

$f(x) = g(x)^2 + 2g(x) + 10$ 
와 같은 식이 있을 때 $f(x)$는 **main함수**고, $g(x)$는 사용자 정의 함수같은 **subfunction**이라고 할 수 있습니다. 매트랩에서 생각을 한다면 ***script를 main 함수의 코드블럭***이라고 생각할 수 있고,  ***그 안에서 작성되는 함수들을 subfunction***이라고 볼 수 있습니다. 따라서 코드가 실행되는 것을 그림으로 표현한다면 다음과 같습니다.

![실행과정](https://user-images.githubusercontent.com/119858743/212460604-fd220eb6-cc82-4699-af91-d472f31009b6.PNG)

당연히 subfunction 안에서도 다른 subfunction을 호출할 수 있고, subfunction안에서 자기자신을 호출할 수도 있습니다. 자기자신을 호출하는 함수를 **재귀함수**라고 부릅니다.

### 재귀함수(Recursion)
재귀함수는 앞서 말했듯이 함수 안에서 자기 자신을 호출하는 함수입니다. 재귀함수로 작성되는 코드는 for문으로도 작성을 할 수 있지만 간결함과 간편함 때문에 재귀함수가 사용됩니다. 재귀함수의 예시를 바로 보겠습니다.
```
function fibbo_return = fibbo(num)
    if num == 0 || num == 1
        fibbo_return = 1;
        return 
    end

    fibbo_return = fibbo(num-1) + fibbo(num-2);
    return
end
```
위의 예제는 피보나치 수열을 출력하는 함수입니다. 피보나치 수열은 첫째 및 둘째 항이 1이고 그 뒤의 모든 항은 바로 앞 두 항의 합인 수열입니다. 이 함수의 동작방식을 그림으로 설명하면 다음과 같습니다.

![피보나치](https://user-images.githubusercontent.com/119858743/212461554-f22e0535-0d5d-49ac-9302-3bf45f2e2d11.PNG)

각 함수는 매개변수에 들어가는 값을 낮춰서 반복적으로 자기 자신보다 낮은 피보나치 수열을 구하고, 그 값을 더하고 있습니다. 재귀함수를 만들 때 조심해야할 것은 반드시 **하위의 반환 조건**만들어야 한다는 것입니다. 가장 하위의 반환 조건을 만들지 않는다면 반복문에서 무한루프를 도는 것처럼 영원히 계속 자기 자신보다 낮은 함수를 재귀 호출할 것이기 때문입니다.

* [➝Chapter1(프로그래밍이란?) 바로가기](/MATLAB/ProgrammingBackGround.md)
* [➝Chapter2(자료형과 변수) 바로가기](/MATLAB/ProgrammingBackGround2.md)
* [➝Chapter3(입출력) 바로가기](/MATLAB/ProgrammingBackGround3.md)
* [➝Chapter4(연산자) 바로가기](/MATLAB/ProgrammingBackGround4.md)
* [➝Chapter5(조건문) 바로가기](/MATLAB/ProgrammingBackGround5.md)
* [➝Chapter6(반복문) 바로가기](/MATLAB/ProgrammingBackGround6.md)
* [➝Chapter7(분기문) 바로가기](/MATLAB/ProgrammingBackGround7.md)
