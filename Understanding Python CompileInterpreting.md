Understanding Python Compile/Interpreting 
#software-engineering/python

### Understanding Python
#### Compiler VS Interpreter

*~what both these do:~* 
- they transalate to source code to machine lanaguage that the computer can understand

**Compiler:** takes a source code file -> translates it to an -> object file (machine code)
- faster peformance
![](Understanding%20Python%20CompileInterpreting/Screenshot%202025-02-23%20at%2010.41.56%E2%80%AFPM.png)
**Interpreter:** interprets to machine code during run-time 
- reads each source code than transalates.
![](Understanding%20Python%20CompileInterpreting/image.png)

~*is python a compiler or interpreter?:*~
- python is a hybrid - both compiler and interpreter. but mostly an interpreted language 
- python programs become platform indpendent (OS), since they use `pvm` as a middle-man
---
*~how python program runs?:~ 
- Python **compiles to bytecode** and then **interprets that bytecode** at runtime
**Compilation Step**: 
1) When you run a Python program (say, a file called script.py), Python first *compiles* the source code into an intermediate form called **bytecode**.
   - This bytecode isn’t machine code that your computer’s processor can directly execute (like what a traditional compiler for languages like C produces).
   - Instead, it’s a lower-level representation of your program that’s easier for Python to process. This compilation happens automatically and quickly, and the bytecode is typically stored in files with a .pyc extension in a __pycache__ directory.
**Interpretation Step**: 
2) After generating the bytecode, Python uses a **virtual machine** (specifically, the Python Virtual Machine, or PVM) to *interpret* and execute that bytecode line by line.
   - This interpretation is what makes Python an “interpreted language” in practical terms—there’s no separate step where you produce a standalone executable file like you would with a compiled language such as C or Rust.
---
~*what is the use of compiling to bytecode?:*~
* **Speed**: Compiles once, caches as .pyc files, skips re-parsing.
* **Simplicity**: Bytecode is easier for the PVM to execute than raw code.
* **Portability**: Runs on any platform with Python, no machine code needed.
* **Optimization**: Allows basic cleanup and supports tools like PyPy’s JIT.

example of cache:
```cpp
# example.py
x = 10
print(x + 5)
```

When you run python example.py:
1) Python compiles it to bytecode (something like: LOAD_CONST 10, STORE_NAME x, LOAD_NAME x, LOAD_CONST 5, BINARY_ADD, CALL_FUNCTION print).
2) The .pyc file is cached in __pycache__.
3) The PVM interprets the bytecode, producing 15 on your screen.

If you run it again, Python sees the `.pyc` file matches the source (via timestamps/checksums) and skips straight to step 3, saving a bit of time
---