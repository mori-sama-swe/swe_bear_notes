C++ Understanding Vectors/Arrays and How To Manipulate Them
#software-engineering/cpp

Related Topics
- [[C++ Functions]]

### Arrays and Vectors
In C++, **arrays** and **vectors** are two ways to store multiple elements of the same type. 
- While arrays are a fundamental construct, vectors are part of the Standard Template Library (STL) and provide more flexibility.

Comparison Between Arrays and Vectors
| **Feature** | **Arrays** | **Vectors** |
|:-:|:-:|:-:|
| **Size** | Fixed at compile time | Dynamic, grows/shrinks |
| **Memory Allocation** | Contiguous | Contiguous but resizable |
| **Bounds Checking** | None | .at() provides bounds-check |
| **Flexibility** | Low | High |
| **Performance** | Slightly faster (less overhead) | Slightly slower (extra management overhead) |
---
#### Arrays
Characteristics of Arrays:
- arrays are a **fixed** size
- elements are all the same
- stored contiguously in memory - meaning that memory will be allocated in one chunk
- individual elements can be acces by there position or index
- first element is at index [0] / last element is at index [size - 1] 
- there is no`bounds-check` - meaning you cant over the fixed size of the array

##### Manipulating Arrays: 
##### Declaration and Initialization:
```cpp
// Declaration without initialization
int arr[5]; // Array of 5 integers

// Declaration with initialization
int arr[5] = {1, 2, 3, 4, 5};

// Implicit size
int arr[] = {1, 2, 3, 4, 5}; // Compiler determines the size (5)
```

##### Accessing Elements:
Elements in an array can be accessed using the `index`, starting at [0]:
```cpp
int arr[5] = {1,2,3,4,5} 
cout << arr[0]; // Access the first element : 1 
arr[2] = 10;    // Modify the third element : 3
cout << arr[2]; // Access the third element : 10
```

##### Looping Through an Array:
```cpp
for (int i = 0; i < 5; i++) {
    cout << arr[i] << " ";
}
```

##### Getting the Length of an Array:
to calculate length of an array: dividing the total size by the size of one element gives the number of elements in the array. [SizeOf\( \) Understanding](bear://x-callback-url/open-note?id=1CF27F42-C3F6-4062-9BAD-E4E3EDE07FFA)

- sizeof(arr) gives the total size of the array in bytes.
- sizeof(arr[0]) gives the size of one element in bytes.

The result is the total size of the array, which is sizeof(type) * number_of_elements. For example, if int is 4 bytes and the array has 5 elements, the result will be 20.

![](C++%20Understanding%20VectorsArrays%20and%20How%20To%20Manipulate%20Them/Screenshot%202025-01-14%20at%2011.24.52%E2%80%AFPM.png)
The length must be calculated manually using sizeof for static arrays.
This method does not work for dynamically allocated arrays (e.g., using new).

```cpp
#include <iostream>
#include <vector>  // Include the vector library

int main() {
    int hello[5] = {1,2,3,4,5};

    int length_of_hello = sizeof(hello)/sizeof(hello[0]);
    std::cout << "Length of hello: " << length_of_hello << "\n";

    for(int i = 0; i < length_of_hello; i++){
        std::cout << hello[i] << std::endl;
    }
}
```

---

### Vectors

`Vectors` are dynamic arrays from the **STL** that can grow and shrink in size.

##### Declaration and Initialization:
```cpp
#include <vector>

// Declaration
std::vector<int> vec;

// Initialization
std::vector<int> vec1 = {1, 2, 3, 4, 5};
std::vector<int> vec2(5, 10); // Vector of size 5, initialized with 10
```

##### Accessing Elements:
Similar to arrays, elements in a vector can be accessed using **index**.
```cpp
```cpp
#include <vector>

// Declaration
std::vector<int> vec;

// Initialization
std::vector<int> vec1 = {1, 2, 3, 4, 5};
std::vector<int> vec2(5, 10); // Vector of size 5, initialized with 10

cout << vec[0];  // Access the first element : 1
vec[2] = 15;     // Modify the third element : 15
```
we can use `.at( )` for bounds-checked access
```cpp
cout << vec.at(3); // Throws an exception if out of bounds
```

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    // Declare and initialize a vector
    vector<int> primes = {2, 3, 5, 7, 11};

    // Get the length of the vector
    int vectorLength = primes.size();

    // Display the vector elements and its length
    cout << "Vector elements: ";
    for (int prime : primes) {
        cout << prime << " ";
    }
    cout << "\nVector length: " << vectorLength << endl;

    // Add more elements to the vector
    primes.push_back(13);
    primes.push_back(17);

    // Display updated vector and length
    cout << "Updated Vector elements: ";
    for (int prime : primes) {
        cout << prime << " ";
    }
    cout << "\nUpdated Vector length: " << primes.size() << endl;

    return 0;
}
```