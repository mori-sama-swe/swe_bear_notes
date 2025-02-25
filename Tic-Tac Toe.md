Tic-Tac Toe
#projects/cpp

questions:
---
1) when i initialize "board" am i using the same memory-object from the main scope?

- In C++, when you pass a **2D array** to a function, it **does not create a copy**. Instead, it passes a **pointer** to the first element of the array. 

- This means that any changes you make inside the function **directly modify** the array in main().

✔ **Arrays are always passed by reference in functions** (no copying).
✔ Changes inside initializeBoard() **affect the same memory** as main().
✔ This is why we don't need to return board—it's already modified!

```cpp
#include <iostream>
using namespace std;

const int SIZE = 3;

void initializeBoard(char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            board[i][j] = 'X';  // Fill board with 'X'
        }
    }
}

void displayBoard(const char board[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            cout << board[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    char board[SIZE][SIZE];  // Declare board in main

    initializeBoard(board);  // Function modifies it
    displayBoard(board);     // See the changes

    return 0;
}
```
---

2) Why do we use `std::cin.ignore` 

```cpp
cout << "number: ";
cin >> number;

char line[256];
cout << "line: ";
cin.getline(line, 256);

cout << endl;
```

when we do `cin` and input our characters and we press `enter` -> the enter adds `\n` to the `cin` buffer, so when we do a `cin.getline()` it automatically stops because get lines only gets characters and not `\n` 

`Whycin.ignore() is Needed:`
1) When you use cin >> variable;, it **only reads up to the first whitespace** (space, tab, or newline) and leaves the remaining input (including \n) **in the input buffer**.

2) If you then call cin.getline(), it might **immediately stop** because the newline character (\n) from the previous input is still in the buffer.

3) cin.getline() stops reading when it encounters \n (default delimiter), so instead of waiting for user input, it reads the leftover \n and stops immediately.

4) To **clear** the leftover newline, we use cin.ignore().


`cin.getline()`:  is a function in C++ used to read an entire line of input, including spaces, until a specified delimiter or until the buffer size limit is reached.

```cpp
cin.getline(char* str, int size);
cin.getline(char* str, int size, char delimiter);
```

```cpp
cin.ignore(numeric_limits<streamsize>::max(), '\n');
```
- this is how we can clear input buffer - without having to explicility input char amount

[When and why do I need to use cin.ignore\(\) in C++?](https://stackoverflow.com/questions/25475384/when-and-why-do-i-need-to-use-cin-ignore-in-c)
[How To Clear The Input Buffer | C++ Tutorial](https://www.youtube.com/watch?v=fcygVtDXanM)

