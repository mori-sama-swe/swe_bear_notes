reversing a string
#leetcode

references:
[[Dynamic Memory Allocation]]

question:
Write a C++ function reverse_string that takes a std::string as input and returns a new std::string with the characters in reverse order. The function should use pointers to perform the reversal.

**Function Signature:**
- `std::string reverse_string(const std::string& str);`

⠀**Input:**
* str: The input string.

⠀**Output:**
The function should return a new string with the characters of str reversed.

**Example:**
```cpp
1 std::string input = "Hello, World!";
2 std::string reversed = reverse_string(input);
4 // reversed should be "!dlroW ,olleH"
```

---
```cpp
std::string reverse_string(const std::string &str){

    int len_of_str = static_cast<int>(str.length());
    char* result = new char[len_of_str + 1];

    for(int i = 0; i < len_of_str; ++i){
        result[i] = str[len_of_str - 1 - i];
    }
    result[len_of_str] = '\0';
    std::string reversed(result);
    delete []result;
    return reversed;
}

std::string reverse_string_test(){
    std::string input = "Hello World";
    std::string reversed = reverse_string(input);
    std::cout << "Reversed: " << reversed << std::endl;
    return input;
}
```
```cpp
std::string reverse_string(const std::string& str) {
    int len_of_str = static_cast<int>(str.length());
    char* result = new char[len_of_str + 1];  // Allocate memory for reversed string + null terminator
    // State: For "Hello", len_of_str = 5, result = [?, ?, ?, ?, ?, ?] (6 uninitialized slots)

    for(int i = 0; i < len_of_str; ++i) {
        result[i] = str[len_of_str - 1 - i];  // Copy characters in reverse order
        // State examples:
        // i = 0: result = ['o', ?, ?, ?, ?, ?]
        // i = 1: result = ['o', 'l', ?, ?, ?, ?]
        // i = 2: result = ['o', 'l', 'l', ?, ?, ?]
        // i = 3: result = ['o', 'l', 'l', 'e', ?, ?]
        // i = 4: result = ['o', 'l', 'l', 'e', 'H', ?]
    }
    
    result[len_of_str] = '\0';  // Add null terminator to make it a valid C-style string
    // State: For "Hello", result = ['o', 'l', 'l', 'e', 'H', '\0']

    std::string reversed(result);
    delete[] result;
    return reversed;
}
```

Explanation:

1. `char* result = new char[len_of_str + 1];`

**what it does:** allocates a charcter array with size of 6 [len_of_str + 1] 
- the `1` is added for the null terminator,
- The +1 adds an extra slot for the null terminator ('\0'), which marks the end of a C-style string. Without it, there’s no room for `\0`, and `std::string reversed(result)` could misbehave (e.g., read random memory).

**state:**
- For "Hello", len_of_str = 5, so result gets 6 slots.
- Initially: result = [?, ?, ?, ?, ?, ?] (uninitialized memory).

---
2. `result[i] = str[ len_of_str - 1 - i];`

**What it does**: Fills result by copying characters from str in reverse order.
**Why the `-1 - i`?**:
* `len_of_str - 1` is the index of the last character in str (zero-based indexing).
  * For "Hello", last character 'o' is at index 4 (since 5 - 1 = 4).

`i` moves backward through str as i increases:
* i = 0: 5 - 1 - 0 = 4 → result[0] = 'o'
* i = 1: 5 - 1 - 1 = 3 → result[1] = 'l'
* i = 2: 5 - 1 - 2 = 2 → result[2] = 'l'
* i = 3: 5 - 1 - 3 = 1 → result[3] = 'e'
* i = 4: 5 - 1 - 4 = 0 → result[4] = 'H'

**State** (step-by-step for "Hello"):
* After i = 0: result = ['o', ?, ?, ?, ?, ?]
* After i = 1: result = ['o', 'l', ?, ?, ?, ?]
* After i = 2: result = ['o', 'l', 'l', ?, ?, ?]
* After i = 3: result = ['o', 'l', 'l', 'e', ?, ?]
* After i = 4: result = ['o', 'l', 'l', 'e', 'H', ?]
---
3. `result[len_of_str] = ‘\0’;`
**What it does**: Places a null terminator at the end of result.

**Why the '\0'?**:
* A C-style string must end with `\0` so that functions (like the std::string constructor) know where it stops.
* Without it, result is just a char array, not a proper string, and std::string reversed(result) might read past the end, causing garbage output or crashes.
* It goes at len_of_str (index 5 for "Hello") because that’s the slot after the last character in the reversed string.
**State**:
* Before: result = ['o', 'l', 'l', 'e', 'H', ?]
* After: result = ['o', 'l', 'l', 'e', 'H', '\0']
* Now result is a valid C-style string: "olleH".

---
### Reversing A String via Pointers

- doing be does not work for special characters

```cpp
std::string reverse_string_by_point(const std::string &str){
    std::string reversed {};

    const char* start = str.c_str(); // pointer to start
    const char* end = start;

    while(*end != '\0'){
        ++end;
    }
    --end; // backs up one memory address to not include '\0`;
    while(end >= start){
        reversed += *end;
        --end;
    }   
    return reversed;
}
```

**Explanation:**

In C++, a pointer (`like const char* end`) is a variable that holds a memory address. Pointer arithmetic lets you move that address to point to different elements in an array:
 
* ++end: Moves the pointer forward by one element (one char, typically 1 byte).
  * end = end + 1
* --end: Moves the pointer backward by one element.
  * end = end - 1

The size of the step depends on the type of the pointer. Since end is a const char*, each increment or decrement moves it by sizeof(char) (usually 1 byte), perfectly matching the layout of a string.

**Getting Pointers to the String**:
* const char* start = str.c_str();
  * c_str() returns a pointer to the null-terminated C-style string held by str.
  * For "Hello", start points to 'H' (the first character).
* const char* end = start;
  * Initialize end to the same starting point; we’ll move it later.

**Finding the End**:
* `while (*end != '\0') { ++end; }`
  * Move end forward until it hits the null terminator ('\0').
  * For "Hello", end moves: 'H' → 'e' → 'l' → 'l' → 'o' → '\0'.
* `--end;`
  * Back up one step to point to the last character ('o'), not the \0.
  * Now start points to 'H', and end points to 'o'.

**Reversing with Pointers**:
* `while (end >= start) { reversed += *end; --end; }`
  * *end dereferences the pointer to get the character it points to.
  * Loop runs:
    * end at 'o': reversed += 'o' → "o"
    * end at 'l': reversed += 'l' → "ol"
    * end at 'l': reversed += 'l' → "oll"
    * end at 'e': reversed += 'e' → "olle"
    * end at 'H': reversed += 'H' → "olleH"
  * Stops when end goes before start.

```cpp
Memory:  'H'  'e'  'l'  'l'  'o'  '\0'
Indices:  0    1    2    3    4    5

1. Initially:        start → 'H', end → 'H'
2. After while loop: start → 'H', end → '\0'
3. After --end:      start → 'H', end → 'o'
```

---
##### Visualizing the Pointer Movement
Let’s visualize the pointer arithmetic with `++end and --end` using the string "Hello" as an example. 
- I’ll show the memory layout, the pointer’s position, and how it moves step-by-step through the code. Since we’re focusing on the while (*end != '\0') { ++end; } loop and the subsequent --end, I’ll break it down with diagrams.


`const char* start = str.c_str();` points to the beginning.
`const char* end = start;` starts at the same place.

```cpp
Index:    0    1    2    3    4    5
Memory:  'H'  'e'  'l'  'l'  'o'  '\0'
Address: 1000 1001 1002 1003 1004 1005  (example addresses, assuming 1 byte per char)
```

```cpp
start → 'H'         end → 'H'
        |                  |
        v                  v
[H]  [e]  [l]  [l]  [o]  [\0]
1000 1001 1002 1003 1004 1005
```

`++end:`
* Moves the pointer forward by 1 byte (size of char).
* Example: From 'H' (1000) to 'e' (1001), then to 'l' (1002), and so on.
* Keeps going until end reaches '\0' (1005).

`--end:`
* Moves the pointer backward by 1 byte.
* Example: From '\0' (1005) to 'o' (1004).
* Adjusts end to point to the last character instead of the null terminator.
---
### Pointer Arithmetic: ++end vs. end = end + 1

* **What They Do**:
  * Both move the pointer end forward by one element in memory.
  * For a const char* end, this means moving forward by sizeof(char) (typically 1 byte), since char is the type being pointed to.
* **How They Work**:
  * ++end: The pre-increment operator increases end by 1 and returns the new value. It’s shorthand for “increment and use the result.”
  * end = end + 1: This explicitly adds 1 to the pointer’s address and assigns the result back to end. It’s the same effect but written out.
* **In Memory**:
  * If end is at address 1000 (pointing to 'H'), both ++end and end = end + 1 move it to 1001 (pointing to 'e').