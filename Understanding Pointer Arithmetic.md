Understanding Pointer Arithmetic 
#software-engineering/cpp

Relation:
1) [[Dynamic Memory Allocation]]
2) [[C++ Pointers and References]]
---
### Understanding Pointer Arithmetic
- assignment expressions
- arithmetic expressions
- comparison expressions

`pointer arithmetic` - only makes sense with `raw arrays`
---
`Pointer arithmetic` in C++ is based on the **size of the data type** that the pointer is pointing to. Unlike regular arithmetic on integers or floating-point numbers, 
- **pointer arithmetic modifies the memory address stored in the pointer, moving it forward or backward by multiples of the size of the type.**

### Basic Operation In Arithmetic Pointers

If ptr is a pointer of type T*, then:
1) **Increment `(ptr + n)`** → Moves n positions forward, where each step is sizeof(T).
2) **Decrement `(ptr - n)`** → Moves n positions backward, each step being sizeof(T).
3) **Pointer Difference `(ptr2 - ptr1)`** → Computes the number of elements between two pointers.
4) **Comparison `(ptr1 < ptr2)`** → Compares addresses in memory.

---
#### Understanding Pointer Arithmetic With an `int` Array
In C++, when you perform `pointer arithmetic` like `ptr + 1`, the pointer moves to the **next memory address** that holds an int.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[3] = {100, 200, 300}; // An array of integers
    int* ptr = arr; // ptr now points to arr[0]

    cout << "Value at ptr: " << *ptr << endl;          // 100
    cout << "Value at ptr + 1: " << *(ptr + 1) << endl; // 200
    cout << "Value at ptr + 2: " << *(ptr + 2) << endl; // 300

    return 0;
}
```

##### Memory Representation
Let's assume arr is stored at memory address 0x1000. If an int takes **4 bytes**, the memory would look like this:
| **Index** | **Value** | **Memory Address** |
|:-:|:-:|:-:|
| arr[0] | 100 | 0x1000 |
| arr[1] | 200 | 0x1004 |
| arr[2] | 300 | 0x1008 |
Now, let's analyze *(ptr + 1).

#### How `ptr + 1` Works:
```cpp
*(ptr + 1);
```

when you write above, the following is interpreted as:
1. `ptr + 1` means:
   - take the memory address stored in `ptr` (0x1000)
   - `1` step means moving by the size of the type EX: (**sizeof(int)**)**, which is **4 bytes**.
   - So, `ptr + 1` becomes 0x1004 (which is arr[1]).

2. `*(ptr + 1)` means:
   * Dereference the value stored at 0x1004, which is **200**.

- ptr + 1 moves to the next integer's memory location (sizeof(int) bytes forward).
- *(ptr + 1) accesses the integer stored at that new address.
---
#### Pointer Subtraction
You can also subtract two pointers to find the **number of elements between them**.
```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {5, 10, 15, 20, 25};
    int* ptr1 = &arr[0]; // Points to arr[0] memory addres
    int* ptr2 = &arr[3]; // Points to arr[3] memory address

    cout << "Distance between pointers: " << ptr2 - ptr1 << " elements" << endl;

    return 0;
}

// Output: Distance between pointers: 3 elements

```

How it Works:
* `ptr2 - ptr1` calculates how many steps are between them.
* `ptr2 - ptr1 = (0x100C - 0x1000) / sizeof(int) = 3`
---
#### Incrementing and Decrementing a Pointer
```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int* ptr = arr; // Points to arr[0]

    cout << "Before incrementing, ptr points to: " << *ptr << endl;
    ptr++; // Move to next integer (4 bytes ahead)
    cout << "After incrementing, ptr points to: " << *ptr << endl;

    ptr--; // Move back (4 bytes behind)
    cout << "After decrementing, ptr points to: " << *ptr << endl;

    return 0;
}
```


---
Example

```cpp
#include <iostream>


void swapPointers(int* ptr1, int* ptr2){

    std::cout << "current memory address of ptr1: " << ptr1 << std::endl;
    std::cout << "current memory address of ptr2: " << ptr2 << std::endl;

    *ptr1 = *ptr1 + *ptr2; // 15 = 5 + 10 
    *ptr2 = *ptr1 - *ptr2; // 5 = 15 - 10
    *ptr1 = *ptr1 - *ptr2; // 10 = 15 - 5

    std::cout << "ptr1: " << *ptr1 << std::endl;
    std::cout << "ptr2: " << *ptr2 << std::endl;
    
    std::cout << "swapped memory address: " << ptr1 << std::endl;
    std::cout << "swapped memory address: " << ptr2 << std::endl;
}

int main(){
    
    int a {5};
    int b {10};
    
    int *ptr1 {nullptr};
    int *ptr2 {nullptr};

    ptr1 = &a;
    ptr2 = &b;

    std::cout << "ptr1 originally is: " << *ptr1 << std::endl;
    std::cout << "ptr2 originally is: " << *ptr2 << std::endl;

    swapPointers(ptr1,ptr2);

    std::cout << "ptr1 should be 10: " << *ptr1 << std::endl;
    std::cout << "ptr2 should be 5: " << *ptr2 << std::endl;

    return 0;
}


ptr1 originally is: 5
ptr2 originally is: 10
current memory address of ptr1: 0x16b222de8
current memory address of ptr2: 0x16b222de4
ptr1: 10
ptr2: 5
swapped memory address: 0x16b222de8
swapped memory address: 0x16b222de4
ptr1 should be 10: 10
ptr2 should be 5: 5
```