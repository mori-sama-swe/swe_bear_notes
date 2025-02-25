Python Arithmetic Operators and Expression
#software-engineering/python

![](Python%20Arithmetic%20Operators%20and%20Expression/image.png)
### Arithmetic Operators
Arithmetic operations are the basic math functions you can perform on numbers in Python. They let you add, subtract, multiply, divide, and more, using simple operators.
- Since Python handles numbers like integers (int) and floats (float) natively, these operations are straightforward and versatile.

```py
# Basic arithmetic operations
add = 5 + 3          # 8 (addition)
sub = 10 - 4         # 6 (subtraction)
mul = 3 * 4          # 12 (multiplication)
div = 10 / 2         # 5.0 (division, always float)
floor_div = 7 // 2   # 3 (floor division, rounds down)
mod = 10 % 3         # 1 (modulus, remainder)
exp = 2 ** 3         # 8 (exponentiation)

# Mixing types
mixed = 5 + 2.0      # 7.0 (int + float = float)
div_int = 3 * 1.5    # 4.5 (multiplication with float)

# Precedence and parentheses
prec = 2 + 3 * 4     # 14 (multiplication first)
parens = (2 + 3) * 4 # 20 (parentheses first)

# Practical examples
price = 10.5
tax = 1.5
total = price + tax  # 12.0 (adding totals)

radius = 5
area = 3.14 * radius ** 2  # 78.5 (area calculation)

num = 17
is_even = num % 2 == 0  # False (checking remainder)

# Augmented assignment
x = 5
x += 3               # 8 (x = x + 3)
x *= 2               # 16 (x = x * 2)

# Non-numeric uses
str_concat = "hello" + "world"  # "helloworld"
str_repeat = "ha" * 3           # "hahaha"
list_concat = [1, 2] + [3]      # [1, 2, 3]
list_repeat = [0] * 4           # [0, 0, 0, 0]
```

---
### Python Expressions

```py
# Simple expressions with arithmetic
add_expr = 5 + 3              # 8 (addition expression)
sub_expr = 10 - 4             # 6 (subtraction)
mul_expr = 3 * 4              # 12 (multiplication)
div_expr = 10 / 2             # 5.0 (division)
exp_expr = 2 ** 3             # 8 (exponentiation)

# Expressions with variables
x = 5
y = 2
var_expr = x + y              # 7 (using variables)
complex_expr = x * y + 3      # 13 (multiple operations)

# Comparison expressions (evaluate to True/False)
comp_expr = x > y             # True (greater than)
equal_expr = x == 5           # True (equality)
not_equal = x != y            # True (inequality)

# Logical expressions
and_expr = (x > 0) and (y < 3)  # True (both conditions true)
or_expr = (x < 0) or (y > 1)    # True (one condition true)
not_expr = not (x == y)          # True (negates False)

# String expressions
str_expr = "Hello" + " " + "World"  # "Hello World" (concatenation)
str_repeat = "ha" * 3               # "hahaha" (repetition)

# List expressions
list_expr = [1, 2] + [3, 4]        # [1, 2, 3, 4] (list concatenation)
list_comp = [x * 2 for x in range(3)]  # [0, 2, 4] (list comprehension)

# Mixed-type expression
mixed_expr = str(x) + " items"      # "5 items" (int to string + concat)

# Conditional (ternary) expression
ternary_expr = "big" if x > 3 else "small"  # "big" (if-else in one line)

# Function call in expression
len_expr = len([1, 2, 3]) + 2       # 5 (function result used in arithmetic)

# Bitwise expressions
bit_and = 5 & 3                     # 1 (binary 101 & 011 = 001)
bit_or = 5 | 3                      # 7 (binary 101 | 011 = 111)
bit_shift = 5 << 1                  # 10 (shift left, 101 becomes 1010)
```