OOP - Classes and Objects
#software-engineering/cpp

~*what is oop?:*~
C++ Object-Oriented Programming (OOP)

`OOP` is a way of designing programs around "objects" instead of just functions or logic. These objects are self-contained units that bundle data (attributes) and behavior (functions) together. 
- C++ supports OOP through features like classes, inheritance, polymorphism, and encapsulation.

~*Encapsulation:*~ objects contain data AND operations that work on that data, abstract data type
- information-hiding: implements-specific logic can be hidden, more abstraction - users of the class code to the inteface, since they do not know the implementation
~*Inheritance:*~
- can create new classes in term of existing classes
- reusability
- polymorphic classes
---
#### Classes and Objects | The Blueprint and The Instances
 
~*what is a class?*~
a `class` in `c++` is like a template or a blueprint for creating `objects`, it defines what an `object` can hold and what it can do

components of a `class`
- blueprint from which objects are created
- a user-defined data-type
- has attributes (data)
- has methods (functions)
- can hide data and methods
- provides a public interface 

*~what is a object?~*

An `object` is an instance of a class—think of it as something built from the blueprint. Once you define a class, you can create as many objects as you want from it.

Example of a `Class`:
```cpp
#include <iostream>
#include <string>
using namespace std;

class Car {
public:  // Access specifier (public means accessible from outside)
    string brand;   // Attribute (data)
    int speed;

    // Constructor (special function to initialize objects)
    Car(string b, int s) {
        brand = b;
        speed = s;
    }

    // Method (function inside class)
    void drive() {
        cout << brand << " is driving at " << speed << " mph!" << endl;
    }
};
```
Car is the class name.
- brand and speed are attributes (data members).
- Car(string b, int s) is a constructor that sets up the object when it’s created.
- drive() is a method (member function) that defines behavior.

Example of a `Objects`:
```cpp
int main() {
    // Creating objects
    Car car1("Toyota", 120);  // Object 1
    Car car2("Ford", 150);    // Object 2

    // Accessing attributes and methods
    cout << car1.brand << endl;  // Output: Toyota
    car1.drive();                // Output: Toyota is driving at 120 mph!
    car2.drive();                // Output: Ford is driving at 150 mph!

    return 0;
}
```
- car1 and car2 are objects of the Car class.
- You use the dot operator (.) to access attributes (car1.brand) or call methods (car1.drive()).
---
#### Declaring a Class and Creating Objects

#### ~Steps To Create A Class:~
1) **Define the Class**: Use the class keyword followed by the class name.
2) **Specify Access**: Use access specifiers (public, private, or protected) to control what’s accessible.
3) **Add Data Members**: These are the variables (attributes) the class will hold.
4) **Add Member Functions**: These are the methods (behaviors) the class can perform, including constructors.
5) **End with a Semicolon**: C++ requires a semicolon (;) after the class definition.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {  // Step 1: Define the class
public:      // Step 2: Access specifier
    string name;  // Step 3: Data member
    int age;

    // Step 4: Constructor (a special member function)
    Dog(string n, int a) {
        name = n;
        age = a;
    }

    // Step 4: Regular member function
    void bark() {
        cout << name << " says: Woof! I am " << age << " years old." << endl;
    }
};  // Step 5: Semicolon

int main() {
    Dog myDog("Buddy", 3);  // Create an object
    myDog.bark();           // Call the method
    return 0;
}
```

Breaking It Down:
* `class Dog`: Declares a class named Dog.
* `public`: Anything after this is accessible from outside the class (e.g., myDog.name or myDog.bark()).
* `string name; int age;`: Data members store the dog’s name and age.
* `Dog(string n, int a)`: Constructor initializes the object with values passed when it’s created.
* `void bark()`: A method that uses the object’s data to do something.
---
#### Accessing Class Members

Accessing class members in C++ depends on how the `objec`t is created (on the stack or heap) and the `access specifiers (public, private, protected)` defined in the class. Let’s break it down clearly with examples, covering both syntax and rules.

Key Rules:
* **Public**: Accessible anywhere using . (stack) or -> (heap).
* **Private**: Only accessible inside the class or via public methods (getters/setters).
* **Protected**: Relevant with inheritance (we can explore that if you want).
* **Pointers**: Use -> for heap objects; . won’t work on pointers directly.

##### ~*Types of Class Members*~
* **Data Members**: Variables inside the class (e.g., int age, string name).
* **Member Functions**: Functions defined in the class (e.g., void bark(), constructors, destructors).

~***Access Specifiers***~
* **public**: Members are accessible from anywhere.
* **private**: Members are only accessible within the class (default for classes).
* **protected**: Like private, but also accessible in derived classes (used with inheritance).

##### Accessing Members of Stack-Allocated Objects
When an object is ~created on the stack (automatic memory), you use the dot operator `(.)` to access its members.~

Example:
- **Dot Operator (.)**`: myDog.name, myDog.bark()— direct access to public members.
- **Private Members**: Can’t access secretID directly; use a public method like getID().
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
public:          // Public members
    string name;
    int age;

    Dog(string n, int a) {  // Constructor
        name = n;
        age = a;
    }

    void bark() {
        cout << name << " says: Woof!" << endl;
    }

private:         // Private members
    int secretID = 42;

public:
    int getID() { return secretID; }  // Public method to access private member
};

int main() {
    Dog myDog("Buddy", 3);  // Stack-allocated object

    // Accessing public data members
    cout << myDog.name << endl;  // Output: Buddy
    myDog.age = 4;               // Modify directly
    cout << myDog.age << endl;   // Output: 4

    // Accessing public member function
    myDog.bark();                // Output: Buddy says: Woof!

    // Accessing private member (won't work directly)
    // cout << myDog.secretID << endl;  // Error: secretID is private
    cout << myDog.getID() << endl;   // Output: 42 (via public method)

    return 0;
}
```

##### Accessing Members of Heap-Allocated Objects
When an object is created on the `heap` *~with new, it’s managed via a pointer, so you use the arrow operator (->) to access members.~*

Example:
- **Arrow Operator (->)**: myDog->name, myDog->bark()—shorthand for (*myDog).name (dereference then access).
- **Memory Management**: Don’t forget delete to free the heap memory.
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
public:
    string name;
    int age;

    Dog(string n, int a) {
        name = n;
        age = a;
    }

    void bark() {
        cout << name << " says: Woof!" << endl;
    }
};

int main() {
    Dog* myDog = new Dog("Rex", 5);  // Heap-allocated object

    // Accessing members with ->
    cout << myDog->name << endl;  // Output: Rex
    myDog->age = 6;               // Modify directly
    cout << myDog->age << endl;   // Output: 6
    myDog->bark();                // Output: Rex says: Woof!

    // Clean up
    delete myDog;

    return 0;
}
```

You can also `dereference a pointer with *` and then use the dot operator, though `->` is more common:
```cpp
Dog* myDog = new Dog("Spot", 2);
cout << (*myDog).name << endl;  // Output: Spot (less common syntax)
(*myDog).bark();                // Output: Spot says: Woof!
delete myDog;
```

##### Accessing Members Inside the Class
Within the `class`, members can access each other directly, regardless of access specifiers:

Example:
- Inside revealSecret(), secretID (private) and name (public) are both accessible without special syntax.
```cpp
class Dog {
private:
    int secretID = 42;
public:
    string name;
    void revealSecret() {
        cout << "Secret ID: " << secretID << endl;  // Private member accessed internally
        cout << "Name: " << name << endl;           // Public member accessed internally
    }
};

int main() {
    Dog myDog;
    myDog.name = "Luna";
    myDog.revealSecret();  // Output: Secret ID: 42  Name: Luna
    return 0;
}
```

##### Static Members (Class-Wide Access)
`Static` members belong to the class itself, not individual `objects`. Use the scope resolution operator `(::)` to access them.

Example:
- `**Dog::totalDogs**`: Accessed via the class name, not an object.
- Static members are shared across all objects of the class.

```cpp
class Dog {
public:
    static int totalDogs;  // Static data member
    string name;

    Dog(string n) {
        name = n;
        totalDogs++;  // Increment on creation
    }

    static void showTotal() {  // Static member function
        cout << "Total dogs: " << totalDogs << endl;
    }
};

// Initialize static member outside class
int Dog::totalDogs = 0;

int main() {
    Dog dog1("Max");
    Dog dog2("Bella");
    Dog::showTotal();      // Output: Total dogs: 2 (access via class name)
    return 0;
}
```

Common Pitfalls:
1) Trying to access private members outside the class:
   - Fix it with a setter:
example:
```cpp
Dog myDog("Buddy", 3);
// myDog.secretID = 99;  // Error: secretID is private
```
```cpp
class Dog {
private:
    int secretID;
public:
    void setID(int id) { secretID = id; }
};
```

---
##### Public and Private (Class Member Access Modifiers
In C++, access modifiers (public, private, and protected) control who can access a class’s members (data and functions). 
- They’re key to encapsulation—one of the core ideas in object-oriented programming—letting you hide or expose parts of a class as needed. I’ll explain each one, how they work, and when to use them, with clear examples.

~*public:*~
* **What it does**: Members are accessible from anywhere—inside the class, outside the class, and in derived classes.
* **When to use**: For the interface of your class—things you want users or other code to interact with (e.g., methods, constructors).
~*private:*~
- **What it does**: Members are only accessible within the class itself. Code outside the class (even derived classes) can’t touch them directly.
- **When to use**: For implementation details—data or helper functions you want to hide to prevent misuse or ensure control.
~*protected:*~
* **What it does**: Members are accessible within the class *and* in derived classes (via inheritance). Outside code still can’t access them.
* **When to use**: When you’re designing a base class and want subclasses to use or modify certain members, but still keep them hidden from the outside world.
---
#### Implementing Member Methods

`Implementing` member methods in C++ involves defining the behavior of a class—how its objects interact with their data or the outside world. 
- These methods are functions declared inside the class and can be implemented either inline (inside the class definition) or separately (outside the class).

Best Practices:
- **Inline for Simple**: Use inline for short, trivial methods (e.g., getters).
- **Separate for Complex**: Put bigger methods outside to keep the class readable.
- **Encapsulation**: Make data private and use methods to access it.
- **Header/Source Split**: In real projects, declare in a .h file and implement in a .cpp file.

##### Declaring vs. Implementing
* **Declaration**: Specify the method’s name, return type, and parameters in the class.
* **Implementation**: Write the actual code for what the method does.

**You can implement methods in two ways:**
~*Inline:*~ Inside the class definition.
- When you define a method inside the class, it’s automatically considered inline (a hint to the compiler to optimize by embedding the code).
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
private:
    string name;
    int age;

public:
    Dog(string n, int a) {  // Constructor (inline)
        name = n;
        age = a;
    }

    void bark() {  // Inline method
        cout << name << " says: Woof!" << endl;
    }

    void growOlder() {  // Inline method
        age++;
        cout << name << " is now " << age << " years old." << endl;
    }
};

int main() {
    Dog myDog("Buddy", 3);
    myDog.bark();       // Output: Buddy says: Woof!
    myDog.growOlder();  // Output: Buddy is now 4 years old.
    return 0;
}
```

~*Separate:*~ Outside the class using the scope resolution operator `(::)`.
- For larger or more complex methods, declare them in the class and implement them outside using the scope resolution operator `(ClassName::)`. 
- This keeps the class definition clean and is common in bigger projects.
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
private:
    string name;
    int age;

public:
    Dog(string n, int a);   // Constructor declaration
    void bark();            // Method declaration
    void growOlder();       // Method declaration
    int getAge();           // Getter declaration
};

// Implementations outside the class
Dog::Dog(string n, int a) {  // Constructor
    name = n;
    age = a;
}

void Dog::bark() {  // Method
    cout << name << " says: Woof!" << endl;
}

void Dog::growOlder() {  // Method
    age++;
    cout << name << " is now " << age << " years old." << endl;
}

int Dog::getAge() {  // Getter
    return age;
}

int main() {
    Dog myDog("Rex", 5);
    myDog.bark();       // Output: Rex says: Woof!
    myDog.growOlder();  // Output: Rex is now 6 years old.
    cout << myDog.getAge() << endl;  // Output: 6
    return 0;
}
```

##### Special Member Methods
Some methods have unique roles and rules for implementation:

###### Constructor
[[C++ Constructors]]
Initializes an object. Can be inline or separate.
```cpp
class Dog {
public:
    string name;
    Dog(string n) : name(n) {}  // Inline with initializer list
};
```

##### Destructor
Cleans up when an object is destroyed (especially important with dynamic memory) or goes out of scope.
```cpp
class Dog {
private:
    int* ptr;
public:
    Dog() { ptr = new int(10); }  // Allocates memory
    ~Dog() { delete ptr; }        // Inline destructor frees memory
};
```

###### Getter/Setter
Control access to private members.
```cpp
class Dog {
private:
    int age;
public:
    void setAge(int a) { if (a >= 0) age = a; }  // Inline setter
    int getAge();  // Declaration
};

int Dog::getAge() { return age; }  // Separate getter
```

###### Static Member Methods
Static methods belong to the class, not an object, and can’t access non-static members directly.
- memory is persistent throught the entire scope
```cpp
class Dog {
private:
    static int totalDogs;
public:
    Dog() { totalDogs++; }
    static void showTotal() {  // Static method
        cout << "Total dogs: " << totalDogs << endl;
    }
};

int Dog::totalDogs = 0;  // Initialize static member

int main() {
    Dog d1, d2;
    Dog::showTotal();  // Output: Total dogs: 2
    return 0;
}
```


###### Using `this` Pointer
Inside member methods, this is an implicit pointer to the current object. Useful when parameters shadow member names.

```cpp
class Dog {
private:
    string name;
public:
    void setName(string name) {
        this->name = name;  // this-> distinguishes member from parameter
    }
    string getName() { return name; }
};

int main() {
    Dog myDog;
    myDog.setName("Spot");
    cout << myDog.getName() << endl;  // Output: Spot
    return 0;
}
```

---
#### Adding More Control With `Private`
By default, class members are private (inaccessible outside the class). You can use `private` explicitly and provide methods to interact with the data:

Example:
- `private`: name and age can’t be accessed directly (e.g., myDog.name would fail).
- `setAge and getAge`: Public methods to safely modify or retrieve private data.
```cpp
#include <iostream>
#include <string>
using namespace std;

class Dog {
private:     // Private data
    string name;
    int age;

public:      // Public interface
    Dog(string n, int a) {  // Constructor
        name = n;
        age = a;
    }

    void setAge(int a) {    // Setter
        if (a >= 0) age = a;  // Basic validation
    }

    int getAge() {          // Getter
        return age;
    }

    void bark() {
        cout << name << " says: Woof! I am " << age << " years old." << endl;
    }
};

int main() {
    Dog myDog("Max", 5);
    // myDog.name = "Rex";  // Error: name is private
    myDog.setAge(6);        // Works: use setter
    cout << myDog.getAge() << endl;  // Output: 6
    myDog.bark();           // Output: Max says: Woof! I am 6 years old.
    return 0;
}
---

