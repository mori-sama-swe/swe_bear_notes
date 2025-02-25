Header Files
#software-engineering/cpp

When you `#include` a file, the content of the included file is inserted at the point of inclusion. This provides a useful way to pull in declarations from another file.

`#include` - with `< >` : are system header files in which the compiler knows where to grab it from
```cpp
#include <iostream>
```
`#include` - with `" "` : tells the compiler to include header files local to the project
```cpp
#include "local"
```

---
`add.h`
```cpp
// 1) We really should have a header guard here, but will omit it for simplicity (we'll cover header guards in the next lesson)

// 2) This is the content of the .h file, which is where the declarations go
int add(int x, int y); // function prototype for add.h -- don't forget the semicolon!
```

`main.cpp`
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
```

`add.cpp`
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.

int add(int x, int y)
{
    return x + y;
}
```

When the preprocessor processes the `#include` add.h" line, it copies the contents of add.h into the current file at that point. 

Because our *add.h* contains a forward declaration for function *add()*, that forward declaration will be copied into *main.cpp*. The end result is a program that is functionally the same as the one where we manually added the forward declaration at the top of *main.cpp*.![](Header%20Files/Screenshot%202025-02-21%20at%2010.12.49%E2%80%AFPM.png)
---
### What Are Header Files?
in C++, header files (typically with a .h or .hpp extension) are used to declare functions, classes, variables, or other entities that you want to share across multiple source files (.cpp files) or reuse in your program. 

Think of them as blueprints or contracts: they tell the compiler what’s available without specifying *how* it’s implemented. The actual implementation usually lives in a corresponding .cpp file.

```cpp
#ifndef TEST_H
#define TEST_H

int pointers();

#endif
```

---
#### Key Components of a Header File

1) Include Guards
These lines prevent the header file from being included multiple times in a single compilation, which could cause errors like redefinition of functions or variables.

```cpp
#ifndef // TEST_H checks if TEST_H is not defined yet.

#define // TEST_H defines TEST_H if it wasn’t already defined, marking this file as "processed."

#endif // closes the guard.
```

`TEST_H` is a unique identifier (a macro) for this header file. By convention, it’s the uppercase filename with _H appended to avoid naming collisions.

- Why is this needed?:  Imagine two files, `a.cpp` and `b.cpp`, both include test.h. Without guards, if a.cpp and b.cpp are compiled together, the compiler would see int pointers(); twice and complain about a duplicate declaration. Include guards ensure it’s only processed once.
---
#### Why Use Header Files?

* **Modularity**: You can share code between files without duplicating it.
* **Abstraction**: Hide implementation details (in .cpp) while exposing only what’s needed (in .h).
* **Reusability**: Write a library once, include its header wherever needed.
* **Organization**: Keep declarations in one place for consistency.
---
#### How Header Files Work in a Program

1) **Inclusion with Include**

To use the declarations in `test.h`, a source file (e.g., main.cpp) includes it like this:
```cpp
#include "test.h"
int main() {
    pointers(); // Compiler knows this exists thanks to test.h
    return 0;
}
```

include “test.h" literally pastes the contents of test.h into main.cpp during preprocessing. The compiler then knows pointers() is a valid function.

---
2) **Separation of Declaration and Definition**

The header file only *declares* int pointers();. The *definition* (what the function does) is typically in a .cpp file, like:

```cpp
// test.cpp
#include "test.h"
int pointers() {
    return 42; // Actual implementation
}
```

This separation keeps code modular: headers provide the interface, and source files provide the implementation.

---
3) **Compilation and Linking**
* When you compile main.cpp and test.cpp, the compiler generates object files (e.g., main.o and test.o).
* The linker then connects the call to pointers() in main.o with its definition in test.o, creating the final executable.
* The header file ensures the compiler knows the function’s signature during compilation, even if the definition is in another file.
---
Example Content

1. Header File: `test.h`
```cpp
#ifndef TEST_H
#define TEST_H

int pointer() // prototype definition

#endif
```

2. Main File: `main.cpp`
```cpp
#include "test.h"

int main(){
	pointers()
	return 0;
}
```

3. Source File: `test.cpp`
```cpp
#include "test.h"
int pointers() {
    int x = 10;
    int* p = &x; // Playing with pointers
    return *p;   // Returns 10
}
```