C++ Understanding Variables / Declaration and Initialization Variables
#software-engineering/cpp

### Understanding Variables:
`variables` : A variable in C++ is an **abstraction of a storage location** in memory. It serves as a **named placeholder** that allows you to store, retrieve, and manipulate data during the runtime of a program.

##### Variables As A Binding To Memory: 
At a low level, a variable binds a name to:
1) **a memory address**: The storage location in RAM where the value resides.

2) **a data type**: Defines how many bytes are reserved and how to interpret the bits (e.g., int, float, char).

3) **a scope and lifetime**: Determines its visibility (e.g., local, global) and how long the variable exists (e.g., static, automatic, or dynamic).
example:
```cpp
int x = 42; // x is bound to an address holding 42 as a 4-byte integer.
```

##### Types of Variables:
C++ has a rich type system:
1) **Primitive Types**: `int, float, double, char.`
2) **Compound Types**: `struct, class, array, enum.`
3) **Pointer Types**: `Raw pointers (int*) and smart pointers (std::unique_ptr, etc.).`
4) **Reference Types**: `T& and T&& for avoiding copies or managing ownership.`
5) **User-Defined Types**: `Encapsulation with classes and structs.`

##### Key Dimensions of Variables in C++:
1) Scope:
   * **local**: Visible only within the block where it is defined. Memory is allocated on the stack.
   * **global/Static**: Accessible across functions or files (depending on linkage). Memory is allocated in the data or BSS segment.
   * **thread-local**: Unique for each thread (e.g., thread_local).
   * **class-memmbers**: Belong to instances or the class itself (static).
  
2) Lifetime:
   - Exist for the duration of the enclosing block.
   - Stored on the stack.
```cpp
void foo() {
    int x = 10; // x exists until the function returns
}
```

3) Static Variables 
   - Scope: The variable is only accessible within the block or function where it is defined.
   - Lifetime: The variable's lifetime extends **throughout the entire duration of the program**.
The value of the static variable is preserved across multiple calls to the function or block.

example:	
- key point: Although count is declared in a local scope, its **lifetime** is global. Its memory persists across function calls.
```cpp
void myFunction() {
    static int count = 0; // Initialized only once
    count++;
    std::cout << "Count: " << count << std::endl;
}

int main() {
    myFunction(); // Count: 1
    myFunction(); // Count: 2
    myFunction(); // Count: 3
    return 0;
}
```

4) Dynamic Variables
   - Managed via new/delete or std::unique_ptr/std::shared_ptr.
   - Useful for flexible lifetime management but should be used sparingly due to potential for memory leaks.
```cpp
int* ptr = new int(42);
delete ptr;
```

##### Understanding the C++ Memory Model
1) **Stack**: Local variables, function calls. Fast, but limited size.
2) **Heap**: Dynamically allocated variables. Flexible, but slower and requires manual management.
3) **Static/Global Memory**: Variables with program-wide lifetime.
4) **Registers**: Variables that the compiler optimizes for CPU register storage.

---
### Variable Declaration and Initialization:
A `variable declaration` : introduces a variable and associates it with a specific **type**. It specifies the variable's **name** and **type** but does not necessarily allocate memory or initialize the variable.

`variable initialization` : refers to the process of assigning an initial value to a variable at the time of its declaration.

example:
```cpp
#include <iostream>

int main() {
    // Declaration Only
    int a;             // Default declaration (Uninitialized - undefined behavior for locals)
    static int b;      // Declaration with zero initialization (static variables only)

    // Declaration and Initialization
    int c(10);         // Direct Initialization
    int d = 20;        // Copy Initialization (Assignment-like syntax)
    int e{30};         // List Initialization (Preferred)
    int f = {40};      // Uniform Initialization (Preferred in some cases)
    int g{};           // Zero Initialization using braces (Preferred)

    // Preferred Methods
    int preferred1{50}; // Modern and safe for any value
    int preferred2{};   // Zero-initialized (Modern and clear)

    // Print variables
    std::cout << "a (declared only, undefined for locals)\n";
    std::cout << "b (declared, zero-initialized static): " << b << "\n";
    std::cout << "c (direct init): " << c << "\n";
    std::cout << "d (copy init): " << d << "\n";
    std::cout << "e (list init): " << e << "\n";
    std::cout << "f (uniform init): " << f << "\n";
    std::cout << "g (brace zero-init): " << g << "\n";
    std::cout << "preferred1: " << preferred1 << "\n";
    std::cout << "preferred2: " << preferred2 << "\n";

    return 0;
}
```
---
##### Static Initialization vs. Dynamic Initialization
* **Static Initialization**: Happens during program startup. Variables are zero-initialized.
* **Dynamic Initialization**: User-provided initializers or constructors are executed at runtime.
---
##### Const and Constexpr:
`const`:

the `const` keyword is used to declare variables whose values **cannot be changed after initialization**. It enforces immutability for the variable.

```cpp
const int x = 42; // x is a constant
// x = 50; // Error: x cannot be modified
```
Key Points:
1) Compile-Time or Runtime Constants:
   * A const variable **can be initialized at runtime or compile-time**.
   * The value must be assigned when the variable is declared, and it cannot be modified afterward.
2) Usage:
   * Prevent accidental modification of a value.
   * Improves code readability and intent.
   * Works with any type: primitive types, pointers, references, and user-defined types.

`constexpr`: 

The `constexpr` keyword is used to define variables, functions, or expressions that are **evaluated at compile-time**. 
- This enables optimization and ensures certain values are resolved during compilation, making programs faster.

Key Points:
1) Compile-Time Requirement:
   - If the input to a constexpr function or variable is not a constant, it behaves like const.
   - constexpr guarantees that the value is computed **at compile time**, provided the input is a compile-time constant.	
2) More Restrictive Than const:
   * All constexpr variables are implicitly const, but not all const variables are constexpr.
3) Usage:
   * Defining **true compile-time constants**.
   * Ensuring certain expressions or functions are evaluated during compilation.

```cpp
constexpr int x = 42; // x is a constant, evaluated at compile time
const int y = 50;     // y might be evaluated at runtime
```