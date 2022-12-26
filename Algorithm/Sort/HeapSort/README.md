``` cpp
//백준 2751
#include <iostream>
#include <vector>
using namespace std;

class heap {
private:

	vector<int> heap_tr;
	int count = 0;
public:
	heap();
	void insert(int a);
	void swapUp(int index);
	void swapDown(int parent);
	int get();
	bool empty();
	void show();

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
