# Heap

### Heap이란?
 **Heap**은 한 노드(node)가 최대 두 개의 자식노드(child node)를 가지면서, 마지막 레벨을 제외한 모든 레벨에서 노드들이 꽉 채워진 **complete binary tree**(완전이진트리)를 기본으로 한다.
 <br><br>
 힙의 속성은 두 가지로, 다음과 같다.
 
 + *heap order property*: 부모 노드가 가진 값이 자식 노드가 가진 값보다 항상 크거다 같음
 + *heap shape property*: Complete binary tree여야 하므로, 항상 왼쪽 부터 tree의 node가 차례대로 채워짐

다음 그림이 바로 최대 힙 속성을 만족하는 자료구조이다.

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
