Const and Pointers
#software-engineering/cpp

### Pointers To Constant
#### What Are Pointers to Constants?

A **pointer to a constant** is a pointer that can point to a value (constant or not), but you’re not allowed to modify that value *through the pointer*.

- how ever the pointer itself can change and point elsewhere

The data being pointed to is treated as "read-only" from the pointer’s perspective. This is distinct from a constant pointer (we’ll clarify the difference later).

```cpp
const int* ptr; // Pointer to a constant integer
```

- `const` int means the integer being pointed to is constant (immutable via ptr).
- `*ptr` is the pointer itself, which can still be reassigned to point elsewhere.

Key Characteristics:

1. **The Data is Read-Only (Through The Pointer):**
- you can’t use `ptr` to change the value it points to

```cpp
int x = 10;
const int* ptr = &x; // ptr to point to x
// *ptr = 20; ERROR
std::cout << *ptr << std::endl;
```

2. **The Pointer Itself Can Change:**
   - while the data is constant, the pointer `ptr` isn’t, you can make it point to a different address:
```cpp
int y = 20;
ptr = &y; // OK: ptr now points to y
std::cout << *ptr << std::endl; // Prints 20
```

3. **Works with Both Const and Non-Const Data**:
   - A const int* can point to a non-constant int (like x above) or a true constant:
```cpp
const int* ptr {nullptr};
const int z = 30;
ptr = &z
```

---
#### Why Use Pointers To Constants?
**Safety**: They enforce that a function or piece of code won’t accidentally modify data it shouldn’t.
**Flexibility**: You can pass both constant and non-constant data to a function expecting a const int*.
**API Design**: Common in function parameters to signal "I’ll read this, but I won’t change it."

```cpp
// test.h
#ifndef TEST_H
#define TEST_H

int pointers(const int* p);

#endif

// test.cpp
#include "test.h"
int pointers(const int* p) {
    // *p = 42; // ERROR: Can’t modify the value
    return *p; // OK: Can read and return it
}

// main.cpp
#include "test.h"
#include <iostream>
int main() {
    int x = 10;
    std::cout << pointers(&x) << std::endl; // Prints 10
    const int y = 20;
    std::cout << pointers(&y) << std::endl; // Prints 20
    return 0;
}
```

#### Deep Dive: Const Correctness

C++’s `const` keyword is all about **const correctness**—ensuring variables and pointers reflect their intended mutability. With pointers to constants:

- The `const` applies to the *type being pointed to* (int), not the pointer itself.
- This is why ptr = &something_else is fine, but *ptr = 42 isn’t.

Don’t confuse a **pointer to a constant** `(const int*)` with a **constant pointer** `(int* const)`:

* **Pointer to Constant**: `const int* ptr`
  * Data is read-only.
  * Pointer can be reassigned.

* **Constant Pointer**: `int* const ptr`
  * Pointer cannot change (locked to one address).
  * Data can be modified through the pointer.

Example:
```cpp
int a = 10, b = 20;
int* const constPtr = &a; // Constant pointer
*constPtr = 15; // OK: Can modify a
// constPtr = &b; // ERROR: Can’t reassign constPtr

const int* ptrToConst = &a; // Pointer to constant
// *ptrToConst = 15; // ERROR: Can’t modify a
ptrToConst = &b; // OK: Can point elsewhere
```

**Compiler Enforcement**: The const is a compile-time check. It doesn’t change how the pointer is stored in memory—it’s just a promise you make to the compiler (and breaking it with hacks like casting can lead to undefined behavior).
