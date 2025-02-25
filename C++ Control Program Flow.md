C++ Control Program Flow
#software-engineering/cpp

### IF Statement

The if statement in C++ is a fundamental control structure used to execute a block of code based on a condition.
- The condition is evaluated as a Boolean expression (true or false). If the condition evaluates to true, the block of code inside the if statement is executed; otherwise, it is skipped.

if the `expression` is true then execute the statement
if the `expressions` is false then skip the statement 

#### Conditional Operators:
| **Operator** | **Meaning**                      |
|:------------:|:--------------------------------:|
| && (AND)     | True if both conditions are true |
| ! (NOT)      | Reverses the truth value         |

syntax:
```cpp
if (condition) {
    // Code to execute if the condition is true
}
```
example:
```cpp
#include <iostream>

int main() {
    int num = 10;

    if (num > 5) {  // Condition is true
        std::cout << "Number is greater than 5." << std::endl;
    }

    return 0;
}

// Output: Number is greater than 5.
```

#### Ternary Operator (?:) as a Short if-else Statements:

The ternary operator (?:) is a shorthand for if-else.
syntax:
```cpp
condition ? expression_if_true : expression_if_false;
```
example:
```cpp
#include <iostream>

int main() {
    int num;
    std::cout << "Enter a number: ";
    std::cin >> num;

    std::cout << (num % 2 == 0 ? "Even" : "Odd") << std::endl;

    return 0;
}
```

#### ELSE-IF Statements:
Sometimes, we need to check multiple conditions in sequence.
```cpp
if (condition1) {
    // Executes if condition1 is true
} else if (condition2) {
    // Executes if condition2 is true
} else {
    // Executes if none of the conditions are true
}
```

#### IF-ELSE Statements:
If the condition is false, we can specify an alternative block of code using else.
syntax:
```cpp
if (condition) {
    // Executes if condition is true
} else {
    // Executes if condition is false
}
```
example:
```cpp
#include <iostream>

int main() {
    int age;
    std::cout << "Enter your age: ";
    std::cin >> age;

    if (age >= 18) {
        std::cout << "You are eligible to vote!" << std::endl;
    } else {
        std::cout << "You are not eligible to vote." << std::endl;
    }

    return 0;
}
```

----
### Switch-Case Statements:
The switch statement in C++ is a control structure used for **multi-way decision making**. It is an alternative to using multiple if-else if conditions when comparing a variable against different constant values.

#### When to Useswitch Over if-else?
✅ **Use** switch **when:**
* Checking a **single variable** against **multiple constant values**.
* Handling **menu selections, days of the week, or user input choices**.
* Optimizing **performance** (especially for large cases).

⠀❌ **Avoid** switch **when:**
* Comparing **ranges of values** (e.g., if (x > 5 && x < 10)).
* Using **floating-point numbers** (float or double are not allowed).
* Evaluating **complex conditions** (logical operators are not supported).

Key Points:
* The expression **must be an integer, character, or enumeration** (no float or double values).
* Each case **must be a constant value**.
* break **prevents fall-through** (execution of subsequent cases).
* default **handles unmatched cases** (optional but recommended).

syntax:
```cpp
switch (expression) {
    case value1:
        // Code to execute if expression == value1
        break;
    case value2:
        // Code to execute if expression == value2
        break;
    ...
    default:
        // Code to execute if none of the cases match
}
```

example:
```cpp
#include <iostream>

int main() {
    int day;
    std::cout << "Enter a day number (1-7): ";
    std::cin >> day;

    switch (day) {
        case 1:
            std::cout << "Monday" << std::endl;
            break;
        case 2:
            std::cout << "Tuesday" << std::endl;
            break;
        case 3:
            std::cout << "Wednesday" << std::endl;
            break;
        case 4:
            std::cout << "Thursday" << std::endl;
            break;
        case 5:
            std::cout << "Friday" << std::endl;
            break;
        case 6:
            std::cout << "Saturday" << std::endl;
            break;
        case 7:
            std::cout << "Sunday" << std::endl;
            break;
        default:
            std::cout << "Invalid day number!" << std::endl;
    }

    return 0;
}
```

#### Switch Without The Break (Fall Through Behavior)

If you omit break, execution **falls through** to the next case.
example:
- Since break is missing, all cases **after** 1 are executed.
```cpp
#include <iostream>

int main() {
    int num;
    std::cout << "Enter a number (1-3): ";
    std::cin >> num;

    switch (num) {
        case 1:
            std::cout << "One" << std::endl;
        case 2:
            std::cout << "Two" << std::endl;
        case 3:
            std::cout << "Three" << std::endl;
        default:
            std::cout << "Invalid number!" << std::endl;
    }

    return 0;
}
```
output:
```cpp
Enter a number (1-3): 1
One
Two
Three
Invalid number!
```

#### Switch With Multiple Cases Combined
example:
```cpp
#include <iostream>

int main() {
    char vowel;
    std::cout << "Enter a vowel (a, e, i, o, u): ";
    std::cin >> vowel;

    switch (vowel) {
        case 'a':
        case 'e':
        case 'i':
        case 'o':
        case 'u':
            std::cout << "You entered a vowel!" << std::endl;
            break;
        default:
            std::cout << "Not a vowel!" << std::endl;
    }

    return 0;
}
```
---
### Looping In C++

In C++, loops are used to execute a block of code multiple times based on a condition. There are three primary types of loops:

C++ loops and data types are fundamental for writing efficient programs. Key takeaways:
* for, while, and do-while loops have different use cases.
* `break` stops a loop, `continue` skips an iteration.
* Different data types hold different values with varying memory sizes.
* Nested loops help in processing multi-dimensional data.


#### For Loop: 
The `for loop` is used when the number of iterations is known beforehand.

synatx and example:
```cpp
while (condition) {
    // Loop body
}

#include <iostream>
using namespace std;

int main() {
    int num = 1;
    while (num <= 5) {
        cout << "Number: " << num << endl;
        num++;
    }
    return 0;
}

output:
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5

```

#### While Loop:
the `while` loop is used when the number of iterations is not known in advance and is controlled by a condition

syntax and example:
```cpp
while (condition) {
    // Loop body
}
```

#### Do-While Loop:
The do-while loop is similar to the while loop but executes **at least once**, even if the condition is false.
syntax:
```cpp
do {
    // Loop body
} while (condition);
```

