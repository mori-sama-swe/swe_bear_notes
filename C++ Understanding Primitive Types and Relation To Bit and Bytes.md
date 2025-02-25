C++ Understanding Primitive Types and Relation To Bit and Bytes
#software-engineering/cpp

understanding [bits and bytes and how they are related to primitive types](bear://x-callback-url/open-note?id=C3515289-CAD1-47AB-8F6D-E3F95BC909B8)

### Understanding Primitive Types

`primitive data types`:  are the basic building blocks of data representation in the language. They include integers, floating-point numbers, characters, and boolean types. 
- These types can have **signed** or **unsigned** qualifiers, affecting the range of values they can represent.
---
examples of ypes: 
1) Integer Types
   - Used to represent whole numbers.
| **Type** | **Size (bytes)** | **Typical Range** |
|:-:|:-:|:-:|
| short | 2 | -32,768 to 32,767 |
| int | 4 | -2,147,483,648 to 2,147,483,647 |
| long | 4 or 8 | Platform-dependent |
| long long | 8 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
2. Floating-Point Types
   - Used to represent numbers with decimal points.
| **Type** | **Size (bytes)** | **Precision** | **Range** |
|:-:|:-:|:-:|:-:|
| float | 4 | 7 decimal digits | ~3.4e-38 to ~3.4e+38 |
| double | 8 | 15 decimal digits | ~1.7e-308 to ~1.7e+308 |
| long double | 8, 10, or 16 | 18+ decimal digits (platform-dependent) | Extended range |
3. Character Type
   - Used to represent single characters.
| **Type** | **Size (bytes)** | **Typical Range** |
|:-:|:-:|:-:|
| char | 1 | -128 to 127 (signed) / 0 to 255 (unsigned) |
4. Boolean Type
   - Used to represent true or false.
| **Type** | **Size (bytes)** | **Possible Values** |
|:-:|:-:|:-:|
| bool | 1 | true or false |
---
##### Signed vs. Unsigned

What Does "Signed" and "Unsigned" Mean?
* **Signed Data Types**: Can store both positive and negative values.
* **Unsigned Data Types**: Can only store non-negative values, doubling the positive range of the corresponding signed type.

```cpp
#include <iostream>
using namespace std;

int main() {
    // Signed data types (default behavior for most types)
    signed int signedInt = -42;          // Integer with negative value
    signed short signedShort = -32000;  // Short integer
    signed long signedLong = -123456789L;  // Long integer
    signed char signedChar = 'A';       // Character (ASCII code 65)

    // Unsigned data types
    unsigned int unsignedInt = 42;      // Integer without negative value
    unsigned short unsignedShort = 32000; // Short integer
    unsigned long unsignedLong = 123456789UL; // Long integer
    unsigned char unsignedChar = 255;   // Maximum value for a byte

    // Boolean (primitive, no signed/unsigned distinction)
    bool isTrue = true;

    // Floating-point types (no signed/unsigned distinction)
    float myFloat = 3.14f;
    double myDouble = 3.141592653589793;

    // Display values
    cout << "Signed int: " << signedInt << endl;
    cout << "Unsigned int: " << unsignedInt << endl;

    cout << "Signed short: " << signedShort << endl;
    cout << "Unsigned short: " << unsignedShort << endl;

    cout << "Signed long: " << signedLong << endl;
    cout << "Unsigned long: " << unsignedLong << endl;

    cout << "Signed char (ASCII): " << (int)signedChar << endl;
    cout << "Unsigned char (ASCII): " << (int)unsignedChar << endl;

    cout << "Boolean value: " << isTrue << endl;
    cout << "Float: " << myFloat << endl;
    cout << "Double: " << myDouble << endl;

    return 0;
}
```

#### Unsigned / Signed Conversion - Type Promotion Rules

example:
```cpp
#include "test.h"
#include <iostream>

int find_max_element(int* arr, int size){
    int unsigned max_e {};
    for(int i=0; i < size; ++i){
        if(arr[i] > max_e){
            std::cout << "array element: " << arr[i] << '\n';
            max_e = arr[i];
        }
    }
    return max_e;
}

int find_max_element_test(){

    int arr[] {-12,-23,-45,-67,-49};
    int size = sizeof(arr) / sizeof(arr[0]); // size of elements = size of bytes in the array / size of the first data type in the array

    std::cout << "size of the array: " << size << '\n';
    std::cout << "size of arr: " << sizeof(arr) << '\n';
    
    int a = find_max_element(arr, size);
    return a;
}
```

Now, when you declare max_e as unsigned int (note: int unsigned is syntactically the same as unsigned int in C++), things change. An unsigned int cannot represent negative numbers—it only holds values from 0 to 4,294,967,295 (on a typical 32-bit system). When initialized with unsigned int max_e {}, it starts at 0, just like before.

Here’s the key part: when you compare a signed int (like arr[i]) with an unsigned int (like max_e) in C++, the signed value undergoes *unsigned conversion* due to C++’s type promotion rules.

---
### Type Sizes and Using SizeOf( ):

the `sizeof` operator returns the size of a type or object in bytes, as determined at compile time.

Key Points:
* **Compile-time operator**: sizeof does not evaluate the expression but rather determines its size.
* **Platform-dependent**: Results can vary based on architecture and compiler settings.
* **Useful for arrays**: It can help determine the total size or number of elements in a statically allocated array:

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Size of int: " << sizeof(int) << " bytes\n";
    cout << "Size of unsigned int: " << sizeof(unsigned int) << " bytes\n";
    cout << "Size of float: " << sizeof(float) << " bytes\n";
    return 0;
}
```

Common Scenarios of `SizeOf( )`:

built-in types: 
```cpp
std::cout << sizeof(int) << std::endl; // Size of an `int`
std::cout << sizeof(char) << std::endl; // Size of a `char`
```
The output depends on the implementation and platform. For example:
* int is typically 4 bytes on most systems.
* char is always 1 byte (by definition in the standard).
---
When applied to user-defined types:
```cpp
struct MyStruct {
    int a;
    char b;
};
std::cout << sizeof(MyStruct) << std::endl;
```
The size includes the memory needed for members plus potential padding added for alignment.
---
When applied to an array:
```cpp
int arr[10];
std::cout << sizeof(arr) << std::endl;
```
The result is the total size of the array, **which is sizeof(type) * number_of_elements**. For example, if int is 4 bytes and the array has 10 elements, the result will be 40.
---
