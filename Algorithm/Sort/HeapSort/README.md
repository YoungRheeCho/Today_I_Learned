# Heap Sort

### Heap Sort란?
 힙정렬은 Heap이라는 자료구조를 통해 정렬을 하는 것을 의미한다. 이를 이해하기 위해서는 Heap이라는 자료구조에 대해서 알아야 한다.<br>
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

### Heap Sort 코드 구현(c++)

``` cpp
//백준 2751
#include <iostream>
#include <vector>
using namespace std;

class heap {	//heap 자료구조를 구현한 클래스
private:

	vector<int> heap_tr;
	int count = 0;
public:
	heap();
	void insert(int a);
	void swapUp(int index);	//아래에서 위로 올라오며 heapify를 진행
	void swapDown(int parent); //위에서 아래로 내려가며 heapify를 진행
	int get();	//root node를 delete
	bool empty();
	void show();	//배열에 입력된 숫자를 

};

heap::heap() {
	//heap_tr.assign(10000,0);
	heap_tr.reserve(10000);
	heap_tr.push_back(0);
	count = 0;
}

void heap::insert(int a) {
	if (empty()) {
		//heap_tr[1] = a;
		heap_tr.push_back(a);
		count++;
	}

	else {
		int index = count + 1;
		count++;
		heap_tr.push_back(a);
		//heap_tr[index] = a;
		swapUp(index);
	}
}

void heap::swapUp(int index) {
	if (index == 1)
		return;

	int parent = index / 2;
	if (heap_tr[index] < heap_tr[parent]) {
		int temp = heap_tr[index];
		heap_tr[index] = heap_tr[parent];
		heap_tr[parent] = temp;
		swapUp(parent);
	}

	else {
		return;
	}
}

bool heap::empty() {
	if (count == 0)
		return true;
	else
		return false;
}

int heap::get() {
	if (count < 1)
		return 0;

	int return_value = heap_tr[1];
	heap_tr[1] = heap_tr[count];
	count--;

	swapDown(1);
	return return_value;
}

void heap::show() {
	for (int i = 1; i <= count; i++) {
		cout << heap_tr[i] << " ";
	}

}

void heap::swapDown(int parent) {	
	int child1 = parent * 2;
	int child2 = parent * 2 + 1;
	int Big_child;

	if (child1 <= count && child2 <= count) {
			Big_child  = heap_tr[child1] <= heap_tr[child2] ? child1 : child2;
	}

	else {
		if (child1 > count && child2 > count)
			return;

		else if (child1 <= count)
			Big_child = child1;

		else if (child2 <= count)
			Big_child = child2;
	
	
	}


	
	if (heap_tr[Big_child] < heap_tr[parent]) {
		int temp = heap_tr[Big_child];
		heap_tr[Big_child] = heap_tr[parent];
		heap_tr[parent] = temp;
		swapDown(Big_child);
	}

	else {
		return;
	}
}


int main() {
	heap testHeap;
	int N{};
	int input;
	cin >> N;

	for (int i = 0; i < N; i++)
	{	
		cin >> input;
		testHeap.insert(input);
	}
	while (!testHeap.empty()) {

		cout << testHeap.get() << "\n";
	}
}
```

[reference](https://ratsgo.github.io/data%20structure&algorithm/2017/09/27/heapsort/)
