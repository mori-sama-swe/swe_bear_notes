C++ Make File Example
#sre/makefile

```makefile
# Compiler
CXX = clang++

# Compiler Flags
CXXFLAGS = -std=c++20 -Wall -Wextra -Wpedantic -O2

# Source files (add all .cpp files)
SRC = main.cpp

# Executable name
TARGET = my_program

# Default rule: Compile and link in one step
all:
	$(CXX) $(CXXFLAGS) -o $(TARGET) $(SRC)

# Clean build files
clean:
	rm -f $(TARGET)

# Rebuild the project
rebuild: clean all

# Run the program
run: all
	./$(TARGET)

.PHONY: all clean rebuild run
```