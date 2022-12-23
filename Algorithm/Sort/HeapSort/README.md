```
#include <iostream>
#include <vector>
using namespace std;
const int a = 10000;

class heap {
private:

	vector<int> heap_tr;
	int count = 0;
public:
	heap();
	void insert(int a);
	void swapUp(int index, int a);
	void swapDown(int parent, int a);
	int get();
	bool empty();

};

heap::heap() {
	heap_tr.assign(10000,0);
	count = 0;
}

void heap::insert(int a) {
	if (empty()) {
		heap_tr[1] = a;
		count++;
	}

	else {
		int index = count + 1;
		heap_tr[index] = a;
		swapUp(index, a);
	}
}

void heap::swapUp(int index, int a) {
	int parent = index / 2;
	if (heap_tr[index] > heap_tr[parent]) {
		int temp = heap_tr[index];
		heap_tr[index] = heap_tr[parent];
		heap_tr[parent] = temp;
		swapUp(parent, heap_tr[parent]);
	}

	else
		return;
}

bool heap::empty() {
	if (count == 0)
		return true;
	else
		return false;
}

int get() {
	


}

void heap::swapDown(int parent, int a) {	

}


int main() {
	vector<int> heap_tr(10);

}
```
