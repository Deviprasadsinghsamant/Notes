# **🔥 Inheritance in C++ – The Ultimate Guide 🚀**

Inheritance is one of the key features of **Object-Oriented Programming (OOP)**. It allows us to **reuse code** by creating a **new class (derived class)** that inherits properties and behavior from an **existing class (base class).**

---

# **📌 4️⃣ Inheritance – Code Reusability in C++**

## ✅ **What is Inheritance?**

🔹 **Inheritance** is a mechanism that allows **one class (child class/derived class)** to acquire the **properties and behaviors** of another class (parent class/base class).  
🔹 It **eliminates redundancy** and **promotes reusability** of code.

### **🎯 Why Use Inheritance?**

✔ **Code Reusability** – Avoid writing the same code multiple times.  
✔ **Improved Maintainability** – Fix errors in one place instead of multiple places.  
✔ **Better Organization** – Organizes similar objects into hierarchical structures.  
✔ **Extensibility** – Add new functionalities while keeping old code intact.

---

## ✅ **Basic Syntax of Inheritance in C++**

```cpp
class BaseClass {
    // Parent class members
};

class DerivedClass : public BaseClass {
    // Child class members (inherits from BaseClass)
};
```

👆 `DerivedClass` **inherits** the properties of `BaseClass` using the `:` symbol.

---

## ✅ **Types of Inheritance in C++**

1️⃣ **Single Inheritance**  
2️⃣ **Multiple Inheritance**  
3️⃣ **Multilevel Inheritance**  
4️⃣ **Hierarchical Inheritance**  
5️⃣ **Hybrid Inheritance**

---

# **📌 1️⃣ Single Inheritance**

**👉 One class inherits from another class.**  
✅ **Base Class** → ✅ **Derived Class**

### **📝 Example:**

```cpp
#include <iostream>
using namespace std;

// Base Class
class Animal {
public:
    void eat() {
        cout << "I can eat!" << endl;
    }
};

// Derived Class (inherits from Animal)
class Dog : public Animal {
public:
    void bark() {
        cout << "I can bark! Woof! Woof!" << endl;
    }
};

int main() {
    Dog myDog;
    
    // Inherited function from Animal class
    myDog.eat();  

    // Function from Dog class
    myDog.bark();  

    return 0;
}
```

✅ **Output:**

```
I can eat!
I can bark! Woof! Woof!
```

---

# **📌 2️⃣ Multiple Inheritance**

**👉 A class inherits from multiple base classes.**  
✅ **Base Class 1 + Base Class 2 → Derived Class**

### **📝 Example:**

```cpp
#include <iostream>
using namespace std;

// Base Class 1
class Father {
public:
    void height() {
        cout << "I am tall!" << endl;
    }
};

// Base Class 2
class Mother {
public:
    void eyeColor() {
        cout << "I have brown eyes!" << endl;
    }
};

// Derived Class (inherits from Father and Mother)
class Child : public Father, public Mother {
public:
    void speak() {
        cout << "I can speak multiple languages!" << endl;
    }
};

int main() {
    Child myChild;

    // Inherited functions
    myChild.height();
    myChild.eyeColor();

    // Function from Child class
    myChild.speak();

    return 0;
}
```

✅ **Output:**

```
I am tall!
I have brown eyes!
I can speak multiple languages!
```

---

# **📌 3️⃣ Multilevel Inheritance**

**👉 A class is derived from another derived class.**  
✅ **Base Class → Derived Class 1 → Derived Class 2**

### **📝 Example:**

```cpp
#include <iostream>
using namespace std;

// Base Class
class Grandparent {
public:
    void grandparentTrait() {
        cout << "I have grey hair!" << endl;
    }
};

// Derived Class 1 (inherits from Grandparent)
class Parent : public Grandparent {
public:
    void parentTrait() {
        cout << "I am hardworking!" << endl;
    }
};

// Derived Class 2 (inherits from Parent)
class Child : public Parent {
public:
    void childTrait() {
        cout << "I love playing video games!" << endl;
    }
};

int main() {
    Child myChild;

    // Inherited functions from both Parent and Grandparent
    myChild.grandparentTrait();
    myChild.parentTrait();
    
    // Function from Child class
    myChild.childTrait();

    return 0;
}
```

✅ **Output:**

```
I have grey hair!
I am hardworking!
I love playing video games!
```

---

# **📌 4️⃣ Hierarchical Inheritance**

**👉 Multiple classes inherit from a single base class.**  
✅ **Base Class → Derived Class 1**  
✅ **Base Class → Derived Class 2**

### **📝 Example:**

```cpp
#include <iostream>
using namespace std;

// Base Class
class Vehicle {
public:
    void fuel() {
        cout << "This vehicle uses fuel!" << endl;
    }
};

// Derived Class 1
class Car : public Vehicle {
public:
    void carFeature() {
        cout << "I have four wheels!" << endl;
    }
};

// Derived Class 2
class Bike : public Vehicle {
public:
    void bikeFeature() {
        cout << "I have two wheels!" << endl;
    }
};

int main() {
    Car myCar;
    Bike myBike;

    // Inherited function
    myCar.fuel();
    myCar.carFeature();

    myBike.fuel();
    myBike.bikeFeature();

    return 0;
}
```

✅ **Output:**

```
This vehicle uses fuel!
I have four wheels!
This vehicle uses fuel!
I have two wheels!
```

---

# **📌 5️⃣ Hybrid Inheritance (Combination of Multiple & Hierarchical)**

Hybrid inheritance is a mix of two or more types of inheritance.

---

# **✅ Access Specifiers in Inheritance**

Access specifiers **(`private`, `protected`, `public`)** determine how members of a base class are inherited by derived classes.

|**Base Class Access**|**Inherited as Public**|**Inherited as Protected**|**Inherited as Private**|
|---|---|---|---|
|`public` members|`public`|`protected`|`private`|
|`protected` members|`protected`|`protected`|`private`|
|`private` members|❌ Not Inherited ❌|❌ Not Inherited ❌|❌ Not Inherited ❌|

---

# **📌 Function Overriding in Inheritance**

Function Overriding allows a derived class to **modify the implementation** of a function from the base class.

### **📝 Example:**

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
    void show() {
        cout << "This is the Parent class." << endl;
    }
};

class Child : public Parent {
public:
    void show() {  // Function overriding
        cout << "This is the Child class." << endl;
    }
};

int main() {
    Child myChild;
    myChild.show();  // Calls the overridden function in Child

    return 0;
}
```

✅ **Output:**

```
This is the Child class.
```

---

# **📖 Layman’s Section – Understanding Inheritance**

Imagine a **parent-child relationship**:

- **Father (Base Class)** has **black hair** and **brown eyes**.
- **Son (Derived Class)** **inherits** these features but can have **additional features like a beard**.

|**Type of Inheritance**|**Real-Life Example**|
|---|---|
|**Single**|Parent → Child|
|**Multiple**|Mother + Father → Child|
|**Multilevel**|Grandparent → Parent → Child|
|**Hierarchical**|Parent → Son, Parent → Daughter|
|**Hybrid**|A combination of the above|

---

# 🎯 **Final Summary**

✅ **Inheritance promotes code reuse and reduces redundancy.**  
✅ **Five types:** Single, Multiple, Multilevel, Hierarchical, Hybrid.  
✅ **Access specifiers control visibility.**  
✅ **Function overriding allows modifying inherited behavior.**

🚀 **Next Steps:**  
Let me know if you want to learn **Polymorphism (Compile-Time & Run-Time Overloading & Overriding)!** 😊