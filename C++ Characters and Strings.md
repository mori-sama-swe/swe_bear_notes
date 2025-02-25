C++ Characters and Strings
#software-engineering/cpp

### Character Functions

`characters functions` - help manipulate and adn analyze individual characters, the `<cctype>` library provides several useful functions

there are functions for `testings` and `converting`

```cpp
#include <cctype>

int main(){
	
	function_name(char) // sytnax
	isalpha('A') // output true
	return 0;
}
```

Some Examples: 
- there are functions for `testings` and `converting`
| **Function** | **Description** | **Example** |
|:-:|:-:|:-:|
| isalpha(ch) | Checks if ch is a letter | isalpha('A') // true |
| isdigit(ch) | Checks if ch is a digit | isdigit('5') // true |
| isalnum(ch) | Checks if ch is a letter or a digit | isalnum('Z') // true |
| isspace(ch) | Checks if ch is a whitespace character | isspace(' ') // true |
| islower(ch) | Checks if ch is lowercase | islower('b') // true |
| isupper(ch) | Checks if ch is uppercase | isupper('G') // true |
| tolower(ch) | Converts ch to lowercase | tolower('A') // 'a' |
| toupper(ch) | Converts ch to uppercase | toupper('b') // 'B' |
```cpp
#include <iostream>
#include <cctype>

int main() {
    char ch = 'A';

    if (isalpha(ch)) {
        std::cout << ch << " is a letter.\n";
    }

    std::cout << "Lowercase: " << (char)tolower(ch) << std::endl;
    std::cout << "Uppercase: " << (char)toupper('b') << std::endl;

    return 0;
}
```
---
### C-Style Strings

**Components of `c-style`:**
Sequence of characters
- contigious or sequenced in memory
- implemented as an array of characters
- terminated by a null character (null)
  - null - character with a value of zero
  - C-style strings are character arrays terminated by a **null character (**\0)

**Declaring and Initializing C-Style Strings**
```cpp
char str1[] = "Hello";  // Implicitly adds '\0'
char str2[6] = "Hello"; // Explicit size including '\0'
char str3[] = {'H', 'e', 'l', 'l', 'o', '\0'}; // Manual definition
```

```cpp
#include <iostream>
#include <cstring>

int main(){
	char my_name[8];
	my_name = "Pat"; // ERROR  - compile error because you can't re-assign an array - you can modify its invidviual contents but not the array name
	strcpy(my_name,"Pat"); // OK 

}
```

##### Why doesmy_name = "Pat"; cause a compile error?
1) **Arrays are not assignable**
* In C, an array name (like my_name) is a constant pointer to its first element.
* This means you **cannot reassign it** like a pointer.
* The statement my_name = "Pat"; attempts to assign a new address to my_name, which is **not allowed**.
2) **How string literals work**
* "Pat" is a **string literal**, which is stored in **read-only memory** (in most modern compilers).
* When you do char *ptr = "Pat";, ptr is assigned the **address** of "Pat" (which is valid because ptr is a pointer).
* But my_name is an **array**, not a pointer, so you **cannot** change its base address.

##### Working with C-Style Strings
The <cstring> library provides functions for manipulating C-style strings:
| **Function** | **Description** | **Example** |
|:-:|:-:|:-:|
| strlen(str) | Returns the length of the string (excluding \0) | strlen("Hello") // 5 |
| strcpy(dest, src) | Copies src into dest | strcpy(dest, "Hi") |
| strncpy(dest, src, n) | Copies n characters from src to dest | strncpy(dest, "Hi", 2) |
| strcat(dest, src) | Appends src to dest | strcat(str1, "World") |
| strncat(dest, src, n) | Appends n characters from src to dest | strncat(str1, "World", 3) |
| strcmp(str1, str2) | Compares str1 and str2 (returns 0 if equal) | strcmp("abc", "abc") // 0 |
| strncmp(str1, str2, n) | Compares the first n characters | strncmp("abc", "abd", 2) // |

Example:
```cpp
#include <iostream>
#include <cstring>

int main() {
    char str1[20] = "Hello";
    char str2[] = "World";

    strcat(str1, " ");  // Adding space
    strcat(str1, str2); // Concatenating "World"

    std::cout << "Concatenated String: " << str1 << std::endl;
    std::cout << "Length: " << strlen(str1) << std::endl;

    return 0;
}
```
---
### C++ Strings

👉 No need to manually allocate or reallocate memory.

C++ proviudes the `std::string` class in <string> for easier string handling
- dynamic size
- work with input and output streams
- lots of useful member functions
- safer
- std namespace
#### Declaring and Initializing Strings
```cpp
#include <iostream>
#include <string>

int main() {
    std::string str1 = "Hello";
    std::string str2("World");
    std::string str3 = str1 + " " + str2; // Concatenation

    std::cout << str3 << std::endl;

    return 0;
}
```

### Usefulstd::string Functions
| **Function** | **Description** | **Example** |
|:-:|:-:|:-:|
| length() or size() | Returns string length | s.length() |
| empty() | Checks if string is empty | s.empty() |
| append(str) | Appends str | s.append("World") |
| insert(pos, str) | Inserts str at pos | s.insert(5, " ") |
| erase(pos, len) | Removes len characters from pos | s.erase(5, 3) |
| substr(pos, len) | Extracts substring | s.substr(0, 3) |
| find(str) | Finds first occurrence of str | s.find("el") |
| replace(pos, len, str) | Replaces part of string | s.replace(0, 3, "Hi") |
```cpp
#include <iostream>
#include <string>

int main() {
    std::string s = "Hello, World!";

    std::cout << "Length: " << s.length() << std::endl;
    std::cout << "Substring: " << s.substr(0, 5) << std::endl;

    s.replace(7, 5, "C++");
    std::cout << "After replace: " << s << std::endl;

    return 0;
}
```

---
#### Choosing Between C-Style and C++ Strings
| **Feature** | **C-Style Strings** | **C++ Strings** |
|:-:|:-:|:-:|
| Memory Management | Requires manual handling (char[]) | Managed automatically (std::string) |
| Functionality | Limited (<cstring> functions) | Rich (std::string methods) |
| Safety | Prone to buffer overflow | Safer with built-in bounds checking |
| Performance | Faster (no overhead) | Slight overhead but more powerful |
**Recommendation:** Use std::string unless you need low-level control (e.g., embedded systems or performance-critical applications).

#### Conclusion:
| **Feature** | **C-Style Strings (**char[]**)** | **C++ Strings (**std::string**)** |
|:-:|:-:|:-:|
| **Memory Management** | Manual (risk of leaks & overflow) | Automatic (prevents leaks & overflow) |
| **String Operations** | Requires <cstring> functions | Rich set of built-in methods |
| **Safety** | No bounds checking | Built-in bounds checking |
| **Comparison** | Uses strcmp() | Direct comparison (==, !=, <, >) |
| **Concatenation** | Uses strcat() | Simple + operator |
| **Ease of Use** | Requires manual handling | High-level abstraction |
| **Iteration** | Uses loops & pointers | Supports iterators & ranged-based loops |
| **I/O Handling** | Requires scanf(), gets() | Supports cin, getline() |
🚀 **Best Practice:** Use std::string in most cases unless you have strict performance or memory constraints requiring C-style strings.

**C-style strings** are simple character arrays terminated with \0 and use <cstring> functions.
**C++ strings (**std::string**)** provide a safer and more flexible way to handle text.
**Character functions** in <cctype> help analyze and manipulate characters.
**Conversions** between std::string and C-style strings allow flexibility.

---
### Looping Over A String and Printing Out Memory Address

In your C++ code, you're printing the memory addresses of individual characters in the string str. Let’s break down why `static_cast<void*>(&str[i])` is necessary here.
```cpp
std::string reverse_string(const std::string &str){
    std::cout << "Memory Address of str: " << &str << '\n';
    std::cout << "Length of str: " << str.length() << '\n';

    for(int i = 0; i < static_cast<int>(str.length()); ++i){
        std::cout << str[i] << " : " << &str[i] << '\n';       
}
```

The expression `&str[i]` gives you the address of the character at index i in the string. Since str is a `std::string`, `str[i]` is a char (or technically a reference to a char), and `&str[i]` is a `char*`—a pointer to a char. 

However, when you try to output this pointer directly with std::cout, you run into a problem: std::cout has an overload for char* that assumes it’s a null-terminated C-style string and tries to print the contents of the memory as a string, starting at that address, rather than the address itself.
