C++ Pointers and References
#software-engineering/cpp

### Passing By Reference

[[C++ Functions]] - in reference:
sometimes we want to be able to change the actual parameter from within the function

in order to achieve this we need the location or address of the actual parameter
- we can use `reference parameters` to tell the compiler to pass in a reference to the actual parameter

In C++, *passing by reference* allows a function to modify the original variable instead of working with a copy. This is done using the `&` symbol in function parameters.

- When a variable is passed by reference, the function operates on the original variable's memory location rather than a copy. 
- This saves memory and enhances performance, especially for large objects like vectors or complex structures.

```cpp
void scale_number(int &num); // prototype

int main(){
	int number {1000};
	scale_number(number); // call
}

void scale_number(int &num){ // definition
	if (num > 100)
		num = 100;
}
```

#### Why Use Pass By Reference?
- **Efficiency:** Avoids copying large objects.
- **Modifications:** Allows functions to modify original values.
- **Avoids Unnecessary Copies:** Saves time, especially for large data structures.
---
```cpp
#include <iostream>
using namespace std;

void modifyValue(int &x) {  // Reference to x
    x = x * 2;  // Modify original value
}

int main() {
    int num = 10;
    cout << "Before: " << num << endl;
    modifyValue(num); // Passing num by reference
    cout << "After: " << num << endl; // num is modified
    return 0;
}
```
```cpp
Before: 10
After: 20
```

Here, the modifyValue function directly modifies num since it is passed by reference.
---
##### Pass by Reference vs Pass by Value
| **Aspect** | **Pass by Value** | **Pass by Reference** |
|:-:|:-:|:-:|
| **Memory Usage** | Creates a copy (more memory) | No copy, modifies original |
| **Performance** | Slower for large objects | Faster (no copy overhead) |
| **Modifies Original?** | No | Yes |
| **Use Case** | Small variables | Large structures or when modification is needed |
---
#### Pass By Reference With `CONST`

If we don’t want a function to modify the argument but still want to avoid copying, we use const.
- The const reference ensures that x cannot be changed inside the function.

```cpp
void printValue(const int &x) {  // Read-only reference
    cout << "Value: " << x << endl;
}

int main() {
    int num = 10;
    printValue(num);  // Safe, cannot modify num
    return 0;
}
```

---
##### Memory Diagram of Pass By Reference
```bash
Before function call:
---------------------
Memory Address | Variable | Value
0x1000        | num      | 10

When function is called (modifyValue(num)):
------------------------------------------
Function `modifyValue(int &x)` gets `x` pointing to `num`'s memory.

Memory Address | Variable | Value
0x1000        | num (x)  | 10  (Before Modification)

Inside Function:
---------------
x = x * 2;

Memory Address | Variable | Value
0x1000        | num (x)  | 20  (Modified)

Function returns:
----------------
The value at address 0x1000 remains modified (20).
```

#### When to Use Pass by Reference?
| **Scenario** | **Use Reference?** |
|:-:|:-:|
| Function modifies input? | ✅ Yes |
| Passing large objects? | ✅ Yes (const &) |
| Read-only input? | ✅ Yes (const &) |
| Passing small variables? | ❌ No (pass by value is fine) |
| Need a nullable variable? | ❌ No (use pointers) |

---
![](C++%20Pointers%20and%20References/image.png)
![](C++%20Pointers%20and%20References/Screenshot%202025-02-10%20at%209.11.54%E2%80%AFPM.png)![](C++%20Pointers%20and%20References/Screenshot%202025-02-10%20at%209.12.52%E2%80%AFPM.png)
- Avoid **returning references to local variables**.
---
### Pointers 

#### What Is A Pointer?
A pointer in C++ is a variable whose value is the memory address of another variable.
- In other words, rather than holding data directly, a pointer holds the location in memory where data is stored.
- This concept is foundational in C++ for several reasons, such as dynamic memory management, efficient array manipulation, and enabling the creation of complex data structures like linked lists and trees.

a `variable` - whose value is an `address`, `pointers` point to variables or functions
- if `x` is a integer variable and its value is `10` then i can declare a `pointer` that points to it
- to use the data that the pointer is pointing to you must know its type
#### Why Use Pointers?:
inside `functions` pointers can be used to access data that defined outside the function.
- those variables may not be in scope so you can’t access them by their name rather there memory
---
#### Declaring Pointers
Declaring pointers in C++ is a straightforward process, but understanding the syntax and its nuances is key to avoiding common pitfalls. Here’s a detailed explanation:

- you read these from right to left to have a better understanding

```cpp
variable_type *pointer_name;
variable_type* ponter_name;

int *int_ptr {nullptr}; // points to no memory address
double *double_ptr_name; // a variable that can point to a type double memory address
```

This declares a `pointer` ptr that can store the address of an int. Note that while many programmers write int* ptr;, you can also write `int *ptr`;
- both are correct, though the first style emphasizes that the pointer's type is "pointer to int."
---
#### Initializing of Pointers
always initialize a pointer before using them, if not it will use `garbage data` or a unwanted memory address being pointed to
- It’s good practice to initialize pointers when you declare them. If you don’t have a valid memory address to assign immediately, you can initialize the pointer to `nullptr`:
- intializing to `zero` or `nullptr` represents address zero<!-- {"fold":true} -->
  - implies its pointing nowhere

```cpp
int* ptr = nullptr;  // ptr is now initialized to point to nothing

int value = 42; 
int* ptr = &value;  // The address-of operator (&) gets the address of 'value' 
```

##### Declaration with Immediate Assignment
Pointers are often declared and initialized in one step, especially when dynamic memory allocation is involved:

```cpp
int* dynamicInt = new int(100);  // dynamically allocates an int with value 100
```

##### Declaration and Assignment of `CONST`
![](C++%20Pointers%20and%20References/Screenshot%202025-02-16%20at%2012.58.18%E2%80%AFPM.png)
---
#### Accessing Pointer Address:

In C++, every variable has its own memory address, including pointers. You can access a pointer's own address (i.e., the address where the pointer is stored) and you can store an address in a pointer using the address-of operator `(&)`. Here’s a detailed explanation:

##### Storing and Address In A Pointer:
Basic Concept:
When you have a variable, say an integer value, you can store its memory address in a pointer. The address-of operator (&) is used to retrieve the address of a variable.
```cpp
int value = 42;                // 'value' is stored at, say, 0x7ffeefbff5a4
int* ptr = &value;             // memory address: 'ptr' now holds the address of 'value' (e.g., 0x0121313)
```
In the above code:
* In this example, imagine that the variable value is located at the memory address 0x7ffeefbff5a4. When we assign ptr = &value;, we store that address in ptr—here represented as 0x0121313 for illustration.
* &value - is the memory addres, lets call this addres x00000, since `ptr` is a pointer that points at a memory address of type int, we are storing the memory address of `value` to `ptr` :: so `ptr` holds the memory address of `value`

##### Typed Pointers
the compiler will make sure that the address stored in a pointer variables is of the correct type
```cpp
int score{10};
double failed{20.1};

int *score_ptr {nullptr};

score_ptr = &score; // OK
score_ptr = &high_temp // Compiler Error
```

##### Accessing a Pointers Own Address:
Every `pointer` variable also resides in memory. To access its own memory address, use the address-of operator (&):
```cpp
int value = 42;                // 'value' at address: 0x7ffeefbff5a4
int* ptr = &value;             // 'ptr' holds address of 'value' (e.g., 0x0121313)
int** ptrToPtr = &ptr;         // 'ptrToPtr' holds address of 'ptr' (e.g., 0x0456789)
```

---
##### Dereferencing a Pointer
`Dereferencing` a pointer means accessing the value stored in the memory location to which the pointer points.
- Instead of dealing with the memory address itself, dereferencing lets you work directly with the value at that address.
- it modifies the value at the address!!!!!

```cpp
int value = 42;              // Suppose 'value' is stored at memory address 0x7ffeefbff5a4
int* ptr = &value;           // 'ptr' holds the address of 'value', e.g., 0x0121313

int dereferencedValue = *ptr;  // Dereferencing 'ptr' retrieves the value 42
```
In this example:
* `&value` gives the memory address of value (for instance, 0x7ffeefbff5a4).
* ptr is declared as a pointer to an int and is assigned that address (illustratively 0x0121313).
* The expression *ptr accesses the value at that memory address, so dereferencedValue will be 42.

example 2:

```cpp

int main(){
int a = 5;
int* ptr1 = &a;
new(ptr1);
}

void new(){
*ptr1 = 10;
}

```
example: 
- It **modifies the value at address** 0x100, meaning a is now 10.
- So, *ptr1 **is like an alias for the actual variable stored at** ptr1**'s address**. That’s why modifying *ptr1 affects a.

**Memory Address vs. Value:** The pointer ptr stores a memory address. When you write `*ptr`, you're not retrieving the address itself but rather the content (the actual value) stored at that memory address.

**Usage in Code:** Dereferencing is crucial for working with dynamically allocated memory, manipulating arrays, and passing values to functions by reference. For example, modifying a value through its pointer:

Always ensure that the pointer you're dereferencing is valid (i.e., it has been properly initialized and points to a valid memory location) to avoid undefined behavior or segmentation faults.

---
### What Is a Reference

refrences must be initalized to a variable when decalred 
- cannot be null
- an alias for a variable

---

