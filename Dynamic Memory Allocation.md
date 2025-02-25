Dynamic Memory Allocation
#software-engineering/cpp

Understandings: 
Heap Memory: [[computer-engineering]]
Pointers and Reference: [[C++ Pointers and References]]
## Dynamic Memory Allocation
Dynamic memory allocation in C++ allows you to request memory during runtime rather than at compile time. 

This is useful when you don't know how much memory you’ll need until the program is running. In C++, 
- you typically use the `new` operator to allocate memory and the `delete` operator to free that memory when it's no longer needed.
- we can use pointers to access newly allocated heap storage
---
### Allocating A Single Type at Run Time

`new` **Operator:** Used for dynamic allocation. Returns a pointer to the allocated memory.

`delete` **Operator:** Used to free memory allocated by new. Use delete for single objects and delete[] for arrays.

`Memory Leaks:` Always deallocate dynamically allocated memory when it's no longer needed to prevent memory leaks.

```cpp
#include <iostream>
using namespace std;

int main() {
    // Allocate memory for a single integer dynamically
    int* ptr = new int; // 'ptr' now points to a memory location for an int

    // Assign a value to the allocated memory
    *ptr = 42; // The allocated integer now holds the value 42

    // Output the value stored in dynamically allocated memory
    cout << "Value: " << *ptr << endl; // Expected output: Value: 42

    // Free the allocated memory to avoid memory leaks
    delete ptr; // 'ptr' is now deallocated

    return 0;
}
```

* **Allocation:** int* ptr = new int; allocates memory for one integer.
* **Assignment:** *ptr = 42; stores the value 42 in that memory.
* **Deallocation:** delete ptr; frees the allocated memory.
---
### Allocating Storagea For An Array

```cpp
#include <iostream>
using namespace std;

int main() {
    int size = 5; // Define the size of the array

    // Dynamically allocate an array of integers using new[]
    int* arr = new int[size]; // arr now points to a block of memory sufficient for 'size' integers

    // Initialize the array elements
    for (int i = 0; i < size; i++) {
        arr[i] = (i + 1) * 10; // For example, arr[0]=10, arr[1]=20, arr[2]=30, arr[3]=40, arr[4]=50
    }

    // Output the array elements
    for (int i = 0; i < size; i++) {
        cout << "arr[" << i << "] = " << arr[i] << endl; // Display each value
    }

    // Deallocate the memory for the array using delete[]
    delete[] arr; // Frees the memory allocated for the array

    // Optionally, set the pointer to nullptr to avoid dangling pointers
    arr = nullptr;

    return 0;
}
```

**Allocation:** `int* arr = new int[size];` allocates memory for an array of int with a length specified by size. The allocated memory is contiguous.

**Initialization:** The loop assigns values to each element. For example, if size is 5, the elements are set to 10, 20, 30, 40, and 50.
- you don't need to explicitly `dereference` when using the array index operator. In C++, when you use `arr[i]`, it's automatically equivalent to `*(arr + i)`. The index operator performs the necessary pointer arithmetic and dereferencing for you.
- `arr[i]` automatically accesses the value stored at the memory location `arr + i`, so no additional dereference operator (*) is needed.

**Accessing Elements:** Elements are accessed using standard array indexing, such as arr[i].

**Deallocation:** `delete[] arr;` frees the memory allocated for the array. Always use delete[] when the memory was allocated with new[] to avoid memory leaks or undefined behavior.

---
### Relationship Between Arrays and Pointers
- the `value` of an array name is the address of the first element in the array
- the `value` of a pointer variable is an address

Example:
```cpp
int scores[] {100,95,89};

std::cout << scores << endl; // 0x61dfec8
std::cout << *scores << endl; // 100

int *score_ptr {scores};

std::cout << score_ptr << endl; //0x61dfec8
std::cout << *score_ptr << endl; // 100
```

#### Understanding Pointer Arithmetic of (PTR + 1) 

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
#### The Array Name As A Pointer
- When you declare an array, its **name acts as a pointer** to the first element in memory.
```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {10, 20, 30, 40, 50};

    cout << "Address of arr (same as &arr[0]): " << arr << endl;
    cout << "Address of arr[0]: " << &arr[0] << endl;
    cout << "Address of arr[1]: " << &arr[1] << endl;
    cout << "Address of arr[2]: " << &arr[2] << endl;
    cout << "Value at arr[0]: " << arr[0] << endl;
    cout << "Value at arr[1]: " << arr[1] << endl;

    return 0;
}
```
**Memory Representation**
| **Array Index** | **Value** | **Memory Address (Hypothetical)** |
|:-:|:-:|:-:|
| arr[0] | 10 | 0x012331 |
| arr[1] | 20 | 0x012335 |
| arr[2] | 30 | 0x012339 |
| arr[3] | 40 | 0x01233D |
| arr[4] | 50 | 0x012341 |
* The name arr holds the address of arr[0] (e.g., 0x012331).
* &arr[1] is located at the next integer address (0x012335 if int is 4 bytes).
* arr[i] is equivalent to *(arr + i), meaning arr[1] is the same as *(arr + 1).
---
#### Assiging an Array to a Pointer

a `pointer` can store the address of an arrasy first element:

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[3] = {100, 200, 300};
    int* ptr = arr; // Equivalent to int* ptr = &arr[0];

    cout << "ptr holds address: " << ptr << endl;  // Address of arr[0]
    cout << "Value at ptr: " << *ptr << endl;      // 100
    cout << "Value at ptr + 1: " << *(ptr + 1) << endl; // 200

    return 0;
}
```
**Memory Representation**
| **Pointer** ptr | **Points to Address** | **Value Stored at Address** |
|:-:|:-:|:-:|
| ptr | 0x012331 | 100 (from arr[0]) |
| ptr + 1 | 0x012335 | 200 (from arr[1]) |
| ptr + 2 | 0x012339 | 300 (from arr[2]) |
