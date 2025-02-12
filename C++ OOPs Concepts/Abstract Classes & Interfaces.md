### **Abstract Classes & Interfaces in C++**

Abstract classes and interfaces are crucial concepts in Object-Oriented Programming (OOP). They help enforce a contract that derived classes must follow, ensuring better code organization, maintainability, and reusability.

---

## **1️⃣ Pure Virtual Functions**

A **pure virtual function** is a function that has no implementation in the base class and must be implemented by any derived class. It is declared using the `= 0` syntax.

### **Example:**

```cpp
#include <iostream>
using namespace std;

// Base class with a pure virtual function
class Shape {
public:
    // Pure virtual function
    virtual void draw() = 0; // Must be implemented by derived classes

    // Regular function
    void info() {
        cout << "This is a shape." << endl;
    }
};

// Derived class implementing the pure virtual function
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Circle." << endl;
    }
};

// Derived class implementing the pure virtual function
class Rectangle : public Shape {
public:
    void draw() override {
        cout << "Drawing a Rectangle." << endl;
    }
};

int main() {
    // Shape s;  // ❌ Error: Cannot instantiate an abstract class

    Circle c;
    Rectangle r;

    c.draw();  // Output: Drawing a Circle.
    r.draw();  // Output: Drawing a Rectangle.

    return 0;
}
```

### **Key Takeaways:**

- A **pure virtual function** (`virtual void draw() = 0;`) forces derived classes to implement it.
- **Abstract classes cannot be instantiated** directly.
- **Derived classes must override all pure virtual functions** before they can be instantiated.

---

## **2️⃣ Abstract Classes**

An **abstract class** is a class that contains at least one pure virtual function. It serves as a blueprint for derived classes.

### **Example:**

```cpp
#include <iostream>
using namespace std;

// Abstract class
class Animal {
public:
    // Pure virtual function
    virtual void makeSound() = 0;

    void sleep() {
        cout << "Sleeping..." << endl;
    }
};

// Derived class implementing the pure virtual function
class Dog : public Animal {
public:
    void makeSound() override {
        cout << "Woof! Woof!" << endl;
    }
};

// Derived class implementing the pure virtual function
class Cat : public Animal {
public:
    void makeSound() override {
        cout << "Meow! Meow!" << endl;
    }
};

int main() {
    // Animal a; ❌ Error: Cannot instantiate an abstract class

    Dog d;
    Cat c;

    d.makeSound(); // Output: Woof! Woof!
    c.makeSound(); // Output: Meow! Meow!

    d.sleep(); // Output: Sleeping...
    c.sleep(); // Output: Sleeping...

    return 0;
}
```

### **Key Takeaways:**

- **Abstract classes contain at least one pure virtual function.**
- **They cannot be instantiated** but can be used as pointers or references.
- **Derived classes must implement all pure virtual functions** to become instantiable.
- **Abstract classes can have normal functions** (like `sleep()` in this example).

---

## **3️⃣ Difference Between Abstract Classes & Interfaces**

|Feature|Abstract Class|Interface|
|---|---|---|
|**Purpose**|Serves as a base class|Defines a contract|
|**Contains Variables**|Yes, can have member variables|No, only pure functions|
|**Contains Methods**|Can have normal & pure virtual functions|Only pure virtual functions|
|**Constructor**|Can have constructors|Cannot have constructors|
|**Inheritance**|Supports normal inheritance (`public`, `protected`, `private`)|Only supports public inheritance|
|**Use Case**|When some functionality should be shared|When only a contract is needed|

---

## **4️⃣ Interfaces in C++ (Using Pure Abstract Class)**

C++ does not have a built-in `interface` keyword like Java or C#. Instead, an **interface** is typically implemented using a class that only contains pure virtual functions.

### **Example:**

```cpp
#include <iostream>
using namespace std;

// Interface (Pure Abstract Class)
class IPlayable {
public:
    virtual void play() = 0;  // Pure virtual function
    virtual void pause() = 0; // Pure virtual function
    virtual void stop() = 0;  // Pure virtual function

    // Virtual destructor for proper cleanup
    virtual ~IPlayable() {}
};

// Implementing the interface
class VideoPlayer : public IPlayable {
public:
    void play() override {
        cout << "Playing video..." << endl;
    }

    void pause() override {
        cout << "Video paused." << endl;
    }

    void stop() override {
        cout << "Video stopped." << endl;
    }
};

int main() {
    VideoPlayer player;

    player.play();  // Output: Playing video...
    player.pause(); // Output: Video paused.
    player.stop();  // Output: Video stopped.

    return 0;
}
```

### **Key Takeaways:**

- An **interface** is a class that only has **pure virtual functions**.
- **Interfaces cannot have data members**.
- **A class implementing an interface must implement all its functions**.
- **Useful for enforcing a contract** among multiple classes.

---

## **5️⃣ Layman’s Explanation**

Think of **abstract classes** and **interfaces** like **rules for making a sandwich** 🍔:

- **Abstract Class** = A sandwich recipe with some default ingredients (like bread) and some steps you must define yourself.
- **Interface** = A contract saying, “You must have a sandwich with at least two slices of bread, but you decide what’s inside.”

### **Real-World Example**

Imagine a **Shape** class:

- It says every shape **must have a way to be drawn**, but **doesn't say how**.
- A **Circle** and a **Rectangle** will **define their own way to be drawn**.

Similarly, an **interface** for a remote control (e.g., `IPlayable`) ensures:

- Every media player **must have play, pause, and stop functions**, but each player **implements them differently**.

---

## **Conclusion**

- **Abstract Classes** provide a base class with both implemented and pure virtual functions.
- **Interfaces** enforce a contract by only having pure virtual functions.
- Use **Abstract Classes** when you need some shared functionality.
- Use **Interfaces** when you only need to enforce behavior.

Would you like more real-world examples or another language implementation? 😊