Python Data Types 
#software-engineering/python

### Python Variables
In Python, a `variable` is like a labeled box where you can store a value—think of it as a way to give a name to some data so you can use it later. You create a variable by assigning a value to a name using the = operator. For example:

```python
x = 10
name = "Alice"
is_active = True
```

#### How Do Variables Work?
When you assign a value to a variable, Python does two key things behind the scenes:
1) **Creates an object**: Python creates an object in memory to hold the value (e.g., 10 becomes an integer object).
2) **Binds the name**: The variable name (like x) gets linked to that object. This is called a **reference**. You can think of the variable as a pointer or nickname for the actual data.
---
#### Python Dynamically Typed
~*why is python dynamically typed?:*~ which means you don’t have to declare the type of a variable (like `int` or `string`) - before using it.
- this `type` is determined during runtime - ***based on the value assigned***

```python
x = 10       # x is an integer
x = "Hello"  # Now x is a string
x = 3.14     # Now x is a float
```

~*how to determine type of a variable?:*~ use the function `type(x)` to determine the data-type
example:
```py
x = 10;
type(x); # output = int
```

Trade-Offs:
* **Errors at Runtime**: Since types aren’t checked until the code runs, you might get type-related errors later (e.g., trying to add a string and an integer).
* **Performance**: Dynamic typing can be slower than static typing because Python has to figure out types on the fly.

---
#### Scope of Variables
Variables in Python have a **scope**, which determines where they can be accessed. There are two main scopes to know about:
- **Local Scope**: Variables defined inside a function are local to that function and can’t be accessed outside it.
- **Global Scope**: Variables defined outside any function are global and can be accessed anywhere in your code (though modifying them inside functions requires the global keyword).

Example:
```py
# Global variable
message = "Hello, world!"

def greet():
    # Local variable
    name = "Alice"
    print(message)  # Can access global variable
    print(name)     # Local to this function

greet()
print(name)  # This will raise an error because 'name' is local to greet()
```
---
### Rules for Declaring Variable Names
Python has a set of strict rules that dictate what’s allowed when naming a variable. If you break these, you’ll get a `SyntaxError` or unexpected behavior.

#### Rules for Variable Names
1) **Characters**: Use letters (a-z, A-Z), digits (0-9), and underscores (_).
2) **Start**: Must begin with a letter or underscore, not a digit.
3) **Case-Sensitive**: age and Age are different.
4) **No Special Chars/Spaces**: No @, #, spaces, etc.
5) **No Keywords**: Avoid if, for, True, etc.

Best Practices:
* **Descriptive**: user_age over x.
* **Snake Case**: first_name, not firstName.
* **Constants**: MAX_SIZE.
* **Avoid Single Letters**: Unless in loops (i).

Examples:
* Valid: `score, _temp, MY_VAR`
* Invalid: `2nd`, `user@name` `for`
---
### Python Data Types
![](Python%20Data%20Types/image.png)

#### Key Properties
Some types are mutable, meaning you can change them—list, dict, and set fall here. Others are immutable, so reassignment creates a new object—think int, float, str, tuple, and frozenset. Order matters too: list, tuple, and str are ordered, while dict and set are not.

#### Numeric Types
There are three numeric types. First, int handles whole numbers like 5, -42, or 1000. Next, float covers decimals like 3.14, -0.5, or 2.0. Finally, complex deals with numbers like 3 + 4j that have real and imaginary parts, though it’s less common.

#### **Text Type**
The `str` type is for text, storing sequences of characters. You can write it as "hello", 'Python', or even "" for an empty string, using either single or double quotes.

#### Sequence Types
Python has three sequence types. The list type is an ordered, mutable collection, like [1, 2, "apple"], where you can change items. 

The tuple type is similar but immutable, like (1, "cat", 3.5), locking its contents after creation. Then there’s range, which generates numbers, such as 0 to 4 with range(5), often used in loops.
- `sequenced` types - contain `indices`

#### Mapping Type
The `dict` type stores key-value pairs and is mutable but unordered. An example is {"name": "Alice", "age": 25}, where you access values using keys like my_dict["name"].

#### Set Types
For unique collections, there’s set, an unordered, mutable type like {1, 2, 3} that removes duplicates—so {1, 1, 2} becomes {1, 2}. The frozenset type is the immutable version, like frozenset([1, 2, 3]). 
- `set` do not contain `indices`

---
### Declaring and Initializing Variables
In Python, "declaring" a variable means giving it a name, and "initializing" means assigning it a value for the first time. 
- Unlike some languages where you declare a variable with a type before using it (e.g., int x; in C), **Python combines declaration and initialization into one step because it’s dynamically typed—you don’t specify the type upfront.**

~*How To Declare And Initialize A Variable:*~
To declare and initialize a variable, you use the assignment operator `=`. You write the variable name on the left, the `=` sign, and the value on the right. Python creates the variable and assigns the value in memory at that moment.

```py
x = 10              # Declares 'x' and initializes it with the integer 10
name = "Alice"      # Declares 'name' and initializes it with the string "Alice"
scores = [90, 85]   # Declares 'scores' and initializes it with a list
```

#### Declaring and Initializing Multiple Variables
You can declare and initialize multiple variables at once. Use commas for separate assignments or chain equal signs for the same value:

example:
```py
a, b = 5, 10    # 'a' is 5, 'b' is 10
x = y = 100     # Both 'x' and 'y' are 100
```

---
### Constants

`constants` : They’re variables meant to hold values that don’t change during your program’s run—like a fixed setting or universal truth.
- it’s a convention: you name them in ALL_CAPS to signal they shouldn’t be altered.

```py
PI = 3.14159
MAX_USERS = 100
```

---