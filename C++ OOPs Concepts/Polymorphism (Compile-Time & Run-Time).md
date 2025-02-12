# **🔥 Polymorphism in C++ – The Ultimate Guide 🚀**

Polymorphism is one of the **four pillars of Object-Oriented Programming (OOP)**. It allows a single interface to be used for different types of objects, making code more flexible and reusable.

---

# **📌 5️⃣ Polymorphism – Compile-Time & Run-Time in C++**

## ✅ **What is Polymorphism?**

🔹 **Polymorphism** means **"many forms."**  
🔹 It allows the **same function or operator** to have **different behaviors** depending on the context.  
🔹 There are **two types of polymorphism in C++**:

- **Compile-time Polymorphism** (Static Binding)
- **Run-time Polymorphism** (Dynamic Binding)

---

# **🔷 1️⃣ Compile-Time Polymorphism (Static Binding)**

🔹 **Decided at compile time.**  
🔹 Achieved using **Function Overloading** and **Operator Overloading.**

---

## ✅ **Function Overloading**

**👉 Multiple functions with the same name but different parameters.**

### **📝 Example: Function Overloading**

```cpp
#include <iostream>
using namespace std;

class Math {
public:
    // Function to add two integers
    int add(int a, int b) {
        return a + b;
    }

    // Function to add three integers
    int add(int a, int b, int c) {
        return a + b + c;
    }

    // Function to add two double numbers
    double add(double a, double b) {
        return a + b;
    }
};

int main() {
    Math obj;

    cout << "Sum of 2 and 3: " << obj.add(2, 3) << endl;
    cout << "Sum of 2, 3, and 4: " << obj.add(2, 3, 4) << endl;
    cout << "Sum of 2.5 and 3.5: " << obj.add(2.5, 3.5) << endl;

    return 0;
}
```

✅ **Output:**

```
Sum of 2 and 3: 5
Sum of 2, 3, and 4: 9
Sum of 2.5 and 3.5: 6
```

🔹 **Same function name `add()`, but different parameters.**  
🔹 **Decided at compile time** which function to call.

---

## ✅ **Operator Overloading**

**👉 Allows operators to be redefined for user-defined types.**

### **📝 Example: Operator Overloading**

```cpp
#include <iostream>
using namespace std;

class Complex {
public:
    int real, imag;

    // Constructor
    Complex(int r, int i) {
        real = r;
        imag = i;
    }

    // Overloading the + operator
    Complex operator + (Complex obj) {
        return Complex(real + obj.real, imag + obj.imag);
    }

    // Function to display complex number
    void display() {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(3, 4), c2(1, 2);
    
    Complex sum = c1 + c2; // Using overloaded + operator
    sum.display();

    return 0;
}
```

✅ **Output:**

```
4 + 6i
```

🔹 **The `+` operator is overloaded to add two complex numbers.**  
🔹 **Decided at compile time** which version of `+` to call.

---

# **🔷 2️⃣ Run-Time Polymorphism (Dynamic Binding)**

🔹 **Decided at runtime.**  
🔹 Achieved using **Virtual Functions & Dynamic Binding.**

## ✅ **Virtual Functions & Dynamic Binding**

**👉 Allows derived class to override a function from the base class.**  
**👉 Function call is determined at runtime.**

### **📝 Example: Virtual Function**

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    // Virtual function (runtime polymorphism)
    virtual void makeSound() {
        cout << "Animal makes a sound" << endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override { // Overriding the function
        cout << "Dog barks!" << endl;
    }
};

int main() {
    Animal* animalPtr;  // Pointer of base class
    Dog myDog;

    animalPtr = &myDog;  // Base class pointer points to derived class object
    animalPtr->makeSound();  // Calls Dog's makeSound() due to dynamic binding

    return 0;
}
```

✅ **Output:**

```
Dog barks!
```

🔹 **The function is decided at runtime based on the object type.**  
🔹 **Virtual keyword ensures dynamic binding.**

---

# **📖 Layman’s Section – Understanding Polymorphism**

Imagine a **music player app** that supports different types of files:

- `.mp3`, `.wav`, `.aac`
- All these files **play** when clicked, but the **internal mechanism is different** for each format.
- The **same action (play)** behaves **differently** based on the **file type**.

---

|**Type of Polymorphism**|**Real-Life Example**|
|---|---|
|**Function Overloading**|Calling the same "order()" function in a restaurant, but with different food items.|
|**Operator Overloading**|Using the `+` operator for numbers (2+3) and for text ("Hello" + "World").|
|**Virtual Function**|A parent class defines "makeSound()", but the child class (Dog) makes a barking sound.|

---

# 🎯 **Final Summary**

✅ **Polymorphism allows different behaviors with the same function/operator.**  
✅ **Two types:**  
✔ **Compile-Time Polymorphism** (Function & Operator Overloading).  
✔ **Run-Time Polymorphism** (Virtual Functions & Dynamic Binding).  
✅ **Improves flexibility and code reusability.**

🚀 **Next Steps:**  
Let me know if you want to learn **Abstraction & Interfaces in C++!** 😊