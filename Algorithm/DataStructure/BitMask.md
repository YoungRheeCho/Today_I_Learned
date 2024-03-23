# BitMask(비트마스크)

### BitMask(비트마스크)란?
 **BitMask**는 2진수를 기본으로 하는 컴퓨터의 연산방식을 활용해 자료구조로 사용하는 것이다. 2진수의 각 자리에 1이면 해당 수가 존재하고 0이면 해당 수가 존재하지 않는 것으로 정의함으로써, 따로 배열을 만들지 않고도 정수 하나만으로 데이터를 저장할 수 있다.
 <br><br>
 예를 들면 다음과 같다.
 
 + *1101*: {1, 3, 4}가 저장된 집합
 + *101100101*: {1, 3, 6, 7, 9}가 저장된 집합.

원래라면 1, 3, 4 총 3가지 숫자를 저장하기 위해서는 크기가 3인 배열이 필요한데, 1101은 10진수의 11과 같으므로 11이라는 한 가지 숫자만으로 {1, 3, 4}라는 집합을 포현할 수 있는 것이다.

### 비트 연산
비트마스크로 표현된 집합에서 숫자 n이 포함이 되어있는지를 확인하는 방법은 2<sup>n</sup>이 1인지 0인지를 확인하면 되고, 집합에 숫자를 추가하거나 빼는 행위는 해당 자리를 1로 만들거나 0으로 만들면 된다. 그리고 이러한 연산과정은 흔히 아는 덧셈 혹은 뺄셈과 같은 연산자로 연산하지 않고 **boolean function**을 이용하여 연산한다.

![heap](https://user-images.githubusercontent.com/119858743/209532535-f798e378-1c26-4557-b1e4-37b52abb6d3f.png)
<br>

### Binary tree의 array 구현
binary tree는 child node를 최대 두개를 가질 수 있으므로 parent의 index를 안다면 child node의 array상 index를 구할 수 있고, 반대로 child node의 index로 parent의 index를 구할 수 있다. parent node와 child node의 array상 index는 다음과 같다.
```
child_index1 = 2 * parent_index //(left child)
child_index2 = 2 * parent_index + 1 //(rigth child)

parent_index = child_index1/2 && child_index2/2
```

### Heapify
배열을 heap의 특성을 만족하는 배열로 바꾸는 연산 과정을 Heapify라고 한다. 예시는 다음과 같다.
![heapify](https://user-images.githubusercontent.com/119858743/209534968-20c99587-dd6a-46b1-9ea8-1f5e676760bc.png)
이 과정은 힙에 새로운 node를 추가하거나, 제거할 때 heap의 특성을 유지하기 위해서 필요하다. heap은 complete binary tree여야 하므로 새로운 node가 추가가 되면 항상 마지막 index에 추가가 된 후, 이를 parent node와 비교하며 heapify를 하고 node를 제거할 때는, 마지막 node와 root node의 자리를 바꾸고 root부터 child node들과 비교를 해가며 heapify를 한다.
insert와 delete의 예시는 다음과 같다.

+ insert
![insert](https://user-images.githubusercontent.com/119858743/209535983-66373601-2562-4029-8878-2e9ce47f12bd.png)
<br>

+ delete
![delete](https://user-images.githubusercontent.com/119858743/209536044-082626df-64a5-4e6b-bfc1-bd86eeeafdc7.png)


* [HeapSort 바로가기](/Algorithm/Sort/HeapSort)
* [reference](https://ratsgo.github.io/data%20structure&algorithm/2017/09/27/heapsort/)

