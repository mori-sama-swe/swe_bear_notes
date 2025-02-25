C++ Multidimensional Arrays
#software-engineering/cpp

##### Multidimensional Arrays in C++
A **multidimensional array** in C++ is essentially an array of arrays. It can represent data in a grid-like format (e.g., tables, matrices). The most commonly used form is a 2D array, but you can have arrays with more than two dimensions.

In C++, when you pass a **2D array** to a function, it **does not create a copy**. Instead, it passes a **pointer** to the first element of the array. This means that any changes you make inside the function **directly modify** the array in main().

**Syntax of Arrays:**
```cpp
type arrayName[rows][columns];

const int rows {3};
const int col {4};

int movie_rating [rows][cols];
```

**Initializing a 2D Array:**
```cpp
int matrix[3][4] = {
    {1, 2, 3, 4},   // Row 1
    {5, 6, 7, 8},   // Row 2
    {9, 10, 11, 12} // Row 3
};
```


**Accessing Elements in Multidimensional Arrays:**
You can access elements using their row and column indices:
```cpp
int value = matrix[row][column];
```
```cpp
#include <iostream>
using namespace std;

int main() {
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };

    // Accessing elements
    cout << "Element at row 2, column 3: " << matrix[1][2] << endl;

    // Modifying an element
    matrix[2][3] = 99;
    cout << "Modified element at row 3, column 4: " << matrix[2][3] << endl;

    return 0;
}
```
```cpp
Element at row 2, column 3: 7
Modified element at row 3, column 4: 99
```

**Looping Through Multidimensional Arrays:**
```cpp
#include <iostream>
using namespace std;

int main() {
    int matrix[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };

    cout << "Matrix elements:" << endl;
    for (int i = 0; i < 3; i++) {         // Loop over rows
        for (int j = 0; j < 4; j++) {     // Loop over columns
            cout << matrix[i][j] << " ";  // Access element
        }
        cout << endl;
    }

    return 0;
}
```
```cpp
Matrix elements:
1 2 3 4 
5 6 7 8 
9 10 11 12
```
---
