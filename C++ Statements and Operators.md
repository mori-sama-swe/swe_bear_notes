C++ Statements and Operators
#software-engineering/cpp

### Expressions and Statements:

expressions:
- a sequence of operators and operands that specifies a computation
- computes a value 

```cpp
34 //literal
1.5 + 2.8 //
```

statements:
- a complete line of code that performs an action

```cpp

if ( true):
	perform logic
```

---
### Assignment Operator

In C++, the **assignment operator (**=**)** is used to assign values from one object to another. The assignment operator can be **implicitly** provided by the compiler or explicitly **overloaded** by the programmer for user-defined types (classes and structs).

```cpp
#include <iostream>

class Example {
public:
    int x;
    Example(int val) : x(val) {}

    void display() { std::cout << "Value: " << x << std::endl; }
};

int main() {
    Example obj1(10);
    Example obj2(20);

    obj2 = obj1; // Default assignment operator (shallow copy)

    obj1.display(); // Output: Value: 10
    obj2.display(); // Output: Value: 10 (copied from obj1)

    return 0;
}
```

---
### Arithmetic Operator

Arithmetic operators are used to perform mathematical operations on numeric operands in C++. These operators work with fundamental data types (e.g., int, float, double) and can be overloaded for user-defined types.

![](C++%20Statements%20and%20Operators/Screenshot%202025-01-26%20at%2011.40.06%E2%80%AFPM.png)

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 3;
    
    cout << "Addition: " << (a + b) << endl;        // 13
    cout << "Subtraction: " << (a - b) << endl;     // 7
    cout << "Multiplication: " << (a * b) << endl;  // 30
    cout << "Division: " << (a / b) << endl;        // 3 (Integer division)
    cout << "Modulus: " << (a % b) << endl;         // 1

    double x = 10.5, y = 3.2;
    cout << "Floating Point Division: " << (x / y) << endl;  // 3.28125

    return 0;
}
```

---
### Increment Decrement Operators
The **increment (**++**)** and **decrement (**--**)** operators in C++ are used to increase or decrease the value of a variable by **1**. They are commonly used in loops and arithmetic operations.

There are two types:
	* 	**Prefix increment/decrement** (++x / --x)
	* 	**Postfix increment/decrement** (x++ / x--)

---
**Operator**	**Description**	**Behavior**
++x	Prefix Increment	Increments first, then returns new value
x++	Postfix Increment	Returns value first, then increments
--x	Prefix Decrement	Decrements first, then returns new value
x--	Postfix Decrement	Returns value first, then decrements

---
Examples:

Increment Operator:

Prefix Increment (++x):
- Increases the value first and then returns the updated value.
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;
    int b = ++a;  // a is incremented first, then assigned to b

    cout << "a: " << a << endl; // Output: 6
    cout << "b: " << b << endl; // Output: 6

    return 0;
}
```

Postfix Increment (x++):
- Returns the original value first and then increments the variable
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;
    int b = a++;  // a is assigned to b first, then incremented

    cout << "a: " << a << endl; // Output: 6
    cout << "b: " << b << endl; // Output: 5

    return 0;
}
```

Decrement Operator:

Prefix Decrement (—x):
	* 	Decreases the value first and then returns the updated value.

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;
    int b = --a;  // a is decremented first, then assigned to b

    cout << "a: " << a << endl; // Output: 4
    cout << "b: " << b << endl; // Output: 4

    return 0;
}
```


Postfix Decrement (x—):
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5;
    int b = a--;  // a is assigned to b first, then decremented

    cout << "a: " << a << endl; // Output: 4
    cout << "b: " << b << endl; // Output: 5

    return 0;
}
```

Performance Consideration:
- Prefix (**++x / --x**) is slightly faster** than **Postfix (**x++ / x--**)** because postfix requires a temporary variable to hold the original value before updating.
- This matters more for **non-primitive types** like iterators in STL.
---
### Mixed Type Expressions:

#### Implicit Type Conversions (Type Promotion):

In **C++**, a **mixed-type expression** is an expression that involves operands of different data types. When such an expression is evaluated, **type conversion** (also called **type promotion or type coercion**) occurs automatically to ensure compatibility between the operands.

C++ follows this ranking from lower to higher precision:
	1.	bool → char → short → int → long → long long
	2.	float → double → long double

```cpp
#include <iostream>
using namespace std;

int main() {
    int intVar = 10;
    double doubleVar = 5.5;
    
    double result = intVar + doubleVar;  // int is promoted to double
    cout << "Result: " << result << endl; // Output: 15.5

    return 0;
}
```

Explanation:
	* 	intVar (int) is **promoted** to double because double has a higher precision.
	* 	The expression is evaluated in double, and the result is 15.5.
---
##### Explicit Type Conversion (Type Casting):

Sometimes, we need to **manually** convert data types using **type casting**.
---
#### C++ Type Casting Methods:
Problems with C-Style Cast
	1.	**Unsafe** – It can perform multiple types of conversions (static, reinterpret, and const) without restriction.
	2.	**Less Readable** – Hard to distinguish which type of conversion is occurring.
	3.	**Hard to Debug** – If used incorrectly, debugging errors can be difficu

*C-Style Cast:*
```cpp
double result = (double)10 / 3; // Converts 10 to double before division
```
*Function-Style Cast*:
```cpp
double result = double(10) / 3; 
```

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10, y = 3;
    
    double result1 = x / y;  // Integer division (result = 3)
    double result2 = (double)x / y;  // Type cast to double before division

    cout << "Without casting: " << result1 << endl; // Output: 3
    cout << "With casting: " << result2 << endl;    // Output: 3.33333

    return 0;
}
```
---
#### C++ Cast Operators (Recommended):
	* 	static_cast<type>(value)
	* 	dynamic_cast<type>(value) (For polymorphism)
	* 	const_cast<type>(value) (For removing const modifier)
	* 	reinterpret_cast<type>(value) (For low-level pointer conversion)
Example:

(a) static_cast<> (Recommended for Safe Conversions)
- Used for **safe and well-defined conversions** (e.g., numeric to numeric, pointer upcasting).
```cpp
#include <iostream>
using namespace std;

int main() {
    int intVal = 10, intDiv = 3;

    // Implicit integer division
    double result1 = intVal / intDiv;  // Integer division (10/3 = 3)

    // Using static_cast to force floating-point division
    double result2 = static_cast<double>(intVal) / intDiv; 

    cout << "Without static_cast: " << result1 << endl; // Output: 3.0 (integer division)
    cout << "With static_cast: " << result2 << endl;    // Output: 3.33333 (floating-point division)

    return 0;
}
```

C++ automatically converts smaller types to larger types in mixed-type expressions.
	* 	Use **explicit casting** (static_cast<>) when necessary to avoid unintended results.
	* 	Be aware of **precision loss** when converting double to int.
	* 	When passing arguments to functions, implicit type conversion follows the function’s parameter types.

---
#### Testing For Equality

In C++, testing for equality is typically done using the equality operator (==). Here are some key points and examples:

##### Basic Equality Check
The == operator checks whether two values are equal.
```cpp
#include <iostream>

int main() {
    int a = 5, b = 5, c = 10;
    
    if (a == b) {
        std::cout << "a and b are equal\n";
    }

    if (a != c) {  // `!=` checks for inequality
        std::cout << "a and c are not equal\n";
    }

    return 0;
}
```

##### Floating Point Comparison

Floating-point numbers should not be compared directly due to precision errors. Instead, compare them using a small tolerance (epsilon).

```cpp
#include <iostream>
#include <cmath>

int main() {
    double x = 0.1 * 3;
    double y = 0.3;

    const double epsilon = 1e-9;  // Small tolerance

    if (std::fabs(x - y) < epsilon) {
        std::cout << "x and y are approximately equal\n";
    } else {
        std::cout << "x and y are NOT equal\n";
    }

    return 0;
}
```

##### Comparing Strings:

Use == to compare std::string objects.
```cpp
#include <iostream>
#include <string>

int main() {
    std::string str1 = "hello";
    std::string str2 = "hello";
    std::string str3 = "world";

    if (str1 == str2) {
        std::cout << "str1 and str2 are equal\n";
    }

    if (str1 != str3) {
        std::cout << "str1 and str3 are not equal\n";
    }

    return 0;
}
```

##### Comparing Pointers
Pointers store addresses, so == checks if two pointers point to the same memory location.
```cpp
#include <iostream>

int main() {
    int a = 10;
    int* p1 = &a;
    int* p2 = &a;

    if (p1 == p2) {
        std::cout << "p1 and p2 point to the same location\n";
    }

    return 0;
}
```

---
### Logical Operators
In C++, **logical operators** are used to perform logical operations, typically in conditional statements or boolean expressions. These operators work with boolean values (true or false), returning a boolean result.

Logical operators are essential in C++ for:
✔️ Decision-making in conditions (if, while, for loops).
✔️ Boolean expressions in programs.
✔️ Optimized execution due to **short-circuit evaluation**.

Logical AND &&
- ✅ Returns true only if **both** operands are true.
```cpp
#include <iostream>
using namespace std;

int main() {
    bool a = true, b = false;
    cout << (a && b) << endl;  // Output: 0 (false)
    cout << (a && true) << endl; // Output: 1 (true)
    return 0;
}
```

Logical OR (||)
```cpp
#include <iostream>
using namespace std;

int main() {
    bool a = true, b = false;
    cout << (a || b) << endl; // Output: 1 (true)
    cout << (b || false) << endl; // Output: 0 (false)
    return 0;
}
```

Logical NOT (!)
```cpp
#include <iostream>
using namespace std;

int main() {
    bool a = true;
    cout << !a << endl; // Output: 0 (false)
    cout << !false << endl; // Output: 1 (true)
    return 0;
}
```

##### Short-Circuit Evaluation
C++ logical operators use **short-circuit evaluation**, meaning:
	* 	For && (AND), if the **first operand is** false, the second operand is **not evaluated**.
	* 	For || (OR), if the **first operand is** true, the second operand is **not evaluated**.

```cpp
#include <iostream>
using namespace std;

bool func1() {
    cout << "func1 called" << endl;
    return false;
}

bool func2() {
    cout << "func2 called" << endl;
    return true;
}

int main() {
    cout << (func1() && func2()) << endl; // "func1 called" is printed, but "func2 called" is not.
    return 0;
}
```

---
### Compound Assignments

Advantages of Compound Assignment Operators:
✔ **Concise code**: Reduces redundancy by combining operation and assignment.
✔ **Improved readability**: Easier to understand the intent of the operation.
✔ **Performance optimization**: Can be optimized by compilers for efficiency.

Compound assignment operators make arithmetic, bitwise, and shift operations more efficient in C++. They are widely used in **loops, mathematical expressions, and bitwise manipulations**.

![](C++%20Statements%20and%20Operators/Screenshot%202025-01-27%20at%2012.14.55%E2%80%AFAM.png)

examples:

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 5;

    a += b;  // a = a + b → 10 + 5 = 15
    cout << "a += b: " << a << endl;  // Output: 15

    a -= b;  // a = a - b → 15 - 5 = 10
    cout << "a -= b: " << a << endl;  // Output: 10

    a *= b;  // a = a * b → 10 * 5 = 50
    cout << "a *= b: " << a << endl;  // Output: 50

    a /= b;  // a = a / b → 50 / 5 = 10
    cout << "a /= b: " << a << endl;  // Output: 10

    a %= b;  // a = a % b → 10 % 5 = 0
    cout << "a %= b: " << a << endl;  // Output: 0

    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10, y = 7;

    x &= y;  // x = x & y → 10 & 7 → 1010 & 0111 = 0010 (2)
    cout << "x &= y: " << x << endl;  // Output: 2

    x |= y;  // x = x | y → 2 | 7 → 0010 | 0111 = 0111 (7)
    cout << "x |= y: " << x << endl;  // Output: 7

    x ^= y;  // x = x ^ y → 7 ^ 7 → 0111 ^ 0111 = 0000 (0)
    cout << "x ^= y: " << x << endl;  // Output: 0

    return 0;
}
```
---