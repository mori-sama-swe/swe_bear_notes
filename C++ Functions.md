C++ Functions 
#software-engineering/cpp

a `function` in C++ is block of coe designed to perform a specific task. function make code, modular, reusable, and easier to manage

### Function Definiton

a `function definition` - consists of:  
- return type - unless its  type `void` which means we don’t expect to return anything
- The function name (identifier)
- A parameter list (optional, defines input to the function)
- The function body (code that executes when the function is called)

```cpp
#include <iostream>
using namespace std;

// Function definition
int add(int a, int b) {
    return a + b;  // Returns the sum of a and b
}

int main() {
    int result = add(5, 3);  // Function call
    cout << "Sum: " << result << endl;
    return 0;
}
```

---
### Function Protoypes /  Function Calling: Compiler Needs to Know

Before calling a function, the compiler **must know about its existence**. This can be ensured in 

**two ways**:
1) Define the function before calling it
2) **Use a function prototype** (declaration before main()).

Example without Function Protoype (Incorrect)
```cpp
#include <iostream>
using namespace std;

int main() {
    int result = subtract(10, 5);  // ERROR: Compiler does not know about subtract()
    cout << "Difference: " << result << endl;
    return 0;
}

int subtract(int a, int b) {
    return a - b;
}
```

#### Function Prototype:

A `function prototype` is a declaration of a function that tells the compiler about the function name, return type, and parameters **before its definition**. It allows the function to be called before it is defined.

```cpp
#include <iostream>
using namespace std;

// Function prototype (declaration)
int multiply(int, int);

int main() {
    int result = multiply(4, 5);  // Function call
    cout << "Product: " << result << endl;
    return 0;
}

// Function definition
int multiply(int x, int y) {
    return x * y;
}
```

**Explanation:**
* int multiply(int, int); declares the function **before main()**, so the compiler knows about its existence.
* The actual function is defined **after main()**.
---
### Function Parameters
Function parameters allow passing values to functions. There are **two types**:
* **Pass by Value** (default) → A copy of the argument is passed.
* **Pass by Reference** → The actual variable is passed (changes reflect in the caller).

#### Pass By Value:
```cpp
#include <iostream>
using namespace std;

void modify(int x) {
    x = 100;  // Changes only local copy
}

int main() {
    int a = 10;
    modify(a);
    cout << "Value of a: " << a << endl;  // a remains 10
    return 0;
}
```
**Output:** Value of a: 10 (Unchanged because only a copy was modified)

#### Pass By Reference:

Understand [[C++ Pointers and References]] 

In **pass-by-reference**, we use a reference variable (&x) in the function parameter list. A reference acts as an **alias** for the original variable. This means that when calling the function, we pass the variable **directly**, without using &a.

```cpp
#include <iostream>
using namespace std;

void modify(int &x) {  // Reference parameter
    x = 100;  // Modifies the original variable
}

int main() {
    int a = 10;
    modify(a);
    cout << "Value of a: " << a << endl;  // a is changed to 100
    return 0;
}
```
**Output:** Value of a: 100 (Changed because reference was used)
---
### Return Statement
The `return` statement is used to return a value from a function to the caller.
```cpp
#include <iostream>
using namespace std;

// Function returning a value
double square(double num) {
    return num * num;  // Returns the square of the number
}

int main() {
    double result = square(4.5);
    cout << "Square: " << result << endl;
    return 0;
}
```

**Explanation:**
* square(4.5) calls the function.
* The function returns 4.5 * 4.5 = 20.25, which is stored in result.

---
#### Summary So Far:
**Function Definition**: Contains the function body.

**Function Prototypes**: Declare a function before its call.

**Function Calling**: Compiler needs to know about the function before calling it.

**Function Parameters**: Can be passed **by value** (copy) or **by reference** (original).

**return Statement**: Sends a value back to the caller.
---
### Default Arguments

You can assign **default values** to function parameters, so if arguments are not provided during a call, the function uses the defaults.

- default values can be in the `prototype or defintion`, NOT BOTH
  - best practice - in the `proto-type`
- must appear at the tail end of the parameter list

| **Aspect** | **Details** |
|:-:|:-:|
| **Where to define?** | Only in function prototype or definition, not both. |
| **Ordering rule** | Default parameters must be **rightmost**. |
| **Evaluation time** | At compile-time (not runtime). |
| **Overloading conflicts?** | Can cause ambiguity if not handled properly. |
| **Best use cases** | Logging, constructors, function flexibility, reducing overloading. |

example
```cpp
#include <iostream>
using namespace std;

void greet(string name = "Guest") {  // Default value "Guest"
    cout << "Hello, " << name << "!" << endl;
}

int main() {
    greet();        // Uses default: "Hello, Guest!"
    greet("John");  // Uses provided argument: "Hello, John!"
    return 0;
}
```

##### Constraints on Default Arguments:
![](C++%20Functions/Screenshot%202025-02-09%20at%2010.46.24%E2%80%AFPM.png)
![](C++%20Functions/Screenshot%202025-02-09%20at%2010.46.35%E2%80%AFPM.png)![](C++%20Functions/Screenshot%202025-02-09%20at%2010.47.26%E2%80%AFPM.png)
---
### Function Overloading

Function overloading allows multiple functions with the **same name** but **different parameter lists**. The compiler differentiates them based on the number or types of arguments.
- a type of `polymorphism` 
  - can have same name, but work with different daya types to execute similar behavior

Summary:
| **Concept** | **Explanation** |
|:-:|:-:|
| **Function Overloading** | Multiple functions with the same name but different parameters. |
| **Key Benefit** | Improves code readability and reduces function name duplication. |
| **How to Overload?** | Vary the number or type of parameters. |
| **Not Allowed** | Overloading by return type alone. |
| **Best Use Cases** | Handling different data types, constructors, multiple parameter options. |


example:
```cpp
#include <iostream>
using namespace std;

// Overloaded functions with different parameters
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int main() {
    cout << "Sum (int): " << add(5, 3) << endl;   // Calls int version
    cout << "Sum (double): " << add(5.5, 2.3) << endl; // Calls double version
    return 0;
}
```

#### Syntax of Function Overloading:
```cpp
#include <iostream>
using namespace std;

// Function 1: Adds two integers
int add(int a, int b) {
    return a + b;
}

// Function 2: Adds two doubles (Overloaded version)
double add(double a, double b) {
    return a + b;
}

// Function 3: Adds three integers (Overloaded version)
int add(int a, int b, int c) {
    return a + b + c;
}

int main() {
    cout << "Sum (int): " << add(5, 3) << endl;        // Calls int version
    cout << "Sum (double): " << add(5.5, 2.3) << endl; // Calls double version
    cout << "Sum (three ints): " << add(1, 2, 3) << endl; // Calls 3-param version
    return 0;
}

Sum (int): 8
Sum (double): 7.8
Sum (three ints): 6

```

Use-Case Example: Simplifying Class Design

```cpp
#include <iostream>
using namespace std;

class Car {
private:
    string brand;
    int year;
public:
    // Overloaded constructors
    Car() {  // Default constructor
        brand = "Unknown";
        year = 2022;
    }

    Car(string b) {  // Constructor with one parameter
        brand = b;
        year = 2022;
    }

    Car(string b, int y) {  // Constructor with two parameters
        brand = b;
        year = y;
    }

    void display() {
        cout << "Car: " << brand << " (" << year << ")" << endl;
    }
};

int main() {
    Car car1;              // Default constructor
    Car car2("Toyota");    // Constructor with brand
    Car car3("Honda", 2019); // Constructor with brand and year

    car1.display();
    car2.display();
    car3.display();
    return 0;
}
```
#### Constraints of Function Overloading:

![](C++%20Functions/Screenshot%202025-02-09%20at%2010.52.37%E2%80%AFPM.png)![](C++%20Functions/Screenshot%202025-02-09%20at%2010.53.17%E2%80%AFPM.png)![](C++%20Functions/Screenshot%202025-02-09%20at%2010.53.45%E2%80%AFPM.png)
---
### Passing Arrays To Functions

[[C++ Pointers and References]]

In C++, you can pass an array to a function in different ways. Since arrays are **passed by reference** by default, modifying an array inside a function affects the original array.

we can pass an array to a function by providing square brackets `[]` in the parameter
```cpp
void print_array(int numbers []);
```

```cpp
#include <iostream>
using namespace std;

// Function to print array elements
void printArray(int arr[], int size) {  // arr is treated as a pointer
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]); // Calculate array size

    printArray(numbers, size);  // Pass array to function
    return 0;
}
```
concepts:
- the array elements are NOT copied
- since the array name evaluates to the location of the array in memory - this address is what is copied
- **the functions has no idea how many elements are in the array since all its knows is the location of the first element —** 
  - When you pass an array to a function in C++, the function **only receives the memory address of the first element**. It has no built-in way to determine how many elements are in the array.

Arrays in C++ **decay into pointers** when passed to a function.
This means that arr[] or arr* inside the function is actually a **pointer to the first element**.
The function **does not receive the array size**—only the address of arr[0].

✔️ **Yes, when passing an array, the function only knows the address of the first element (**arr[0]**).**
✔️ **The function does NOT know the size of the array automatically.**
✔️ **Solution:** Always pass the array **size** along with the array.
---
### How Function Calls Work?
A **function call** is a mechanism in C++ that allows a program to execute a block of code that is defined elsewhere. When a function is called, control is transferred from the calling function (caller) to the called function (callee), and after execution, control returns back to the caller.

LIFO - Last In First Out -> Push and Pop

When a function call occurs, the following sequence of operations takes place:
1. **Memory Allocation**: The program allocates memory on the call stack for the function execution.
2. **Argument Evaluation**: The arguments are evaluated and passed to the function parameters.
3. **Stack Frame Creation**:
   * A **stack frame (activation record)** is created for the called function. It stores:
     * Function parameters
     * Return address (location to return after execution)
     * Local variables
4. **Control Transfer**: The control jumps from the calling function to the called function.
5. **Execution of Function Code**: The function body executes.
6. **Return Value Handling** (if applicable): If the function returns a value, it is stored appropriately.
7. **Stack Frame Destruction**: The function's stack frame is removed after execution.
8. **Control Returns**: Execution resumes from where the function was called.

##### Stack Fram Representation
![](C++%20Functions/Screenshot%202025-02-10%20at%209.47.29%E2%80%AFPM.png)
---
### Recursive Functions
A **recursive function** is a function that calls itself in order to solve a problem. Recursion is often used to break down complex problems into smaller subproblems.

#### Structure of a Recursive Function
Every recursive function must have:
1) **Base Case** - A condition that stops the recursion.
2) **Recursive Case** - The function calls itself with modified arguments.

Base Case: `factorial(0) = 1`
Recursive Case: `factorial(n) = n * factorial(n-1)`
```cpp
0! = 1
n! = n * (n-1)!
```

```cpp
unsigned long long factorial(unsigned long long n){
	if (n == 0){
		return 1; // base case			
	}
	return n * factorial(n-1);// recusrive case
}


int main(){
	cout << factorial(8) << "\n";
	return 0;
}
```

Example Fibonacci:
```cpp

unsigned long long fibonacci(unsigned long long n){
	if (n >= 1){
		return n;	// base case
	}
	return fibonacci(n-1) + fibonacci(n-2); // recursion
}

```

Important Notes:
- if recursion doesn’t eventually stop you will have infinite recursion
- recursion can be resource intensive
- remember the base cases(s)
  - it terminaes the recursion
- only use recursive solutions when it make sense

```cpp
#include <iostream>


unsigned long long fibonacci(unsigned long long n);


unsigned long long fibonacci(unsigned long long n){
    if (n == 0){
        return 1; //base case
    }
   return n * fibonacci(n-1); //recursion
   // 3 - fibonacci(3-1) // 2;
   // 2 - fibonacci(2-1) // 1;
   // 1 - fibonacci(1-1) // 0;
   // 0 - fibonacci(0) --> return 0 base case
}

int main(){
    std::cout << fibonacci(3) << '\n';
    std::cout << fibonacci(30) << '\n';
    std::cout << fibonacci(40) << '\n';
    return 0;
}
```
- ![](C++%20Functions/Screenshot%202025-02-15%20at%2010.12.22%E2%80%AFPM.png)
---