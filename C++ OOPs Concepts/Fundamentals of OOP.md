# **🔥 Object-Oriented Programming (OOP) in C++ – Detailed Explanation**

---

# 📌 **1️⃣ Fundamentals of OOP**

## ✅ **What is OOP?**

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes data and behavior into **objects**, rather than just functions and logic. It allows you to model real-world entities in a structured way.

### **Key Features of OOP:**

✔ **Encapsulation** – Bundling data and methods together  
✔ **Abstraction** – Hiding unnecessary details  
✔ **Inheritance** – Reusing code from other classes  
✔ **Polymorphism** – Multiple forms of a function or method

---

## ✅ **Advantages of OOP Over Procedural Programming**

|**Feature**|**Procedural Programming** (C, Pascal)|**Object-Oriented Programming** (C++, Java)|
|---|---|---|
|**Code Reusability**|No code reusability|Uses **Inheritance** to reuse code|
|**Data Security**|No security (Global variables)|Uses **Encapsulation** to hide data|
|**Complexity Handling**|Difficult to manage large programs|Easy to manage using **Objects**|
|**Flexibility & Scalability**|Hard to modify|Easy to extend with **Polymorphism**|
|**Real-World Modeling**|Not suitable for real-world problems|Represents real-world entities using **Classes & Objects**|

---

## **Example: Procedural vs. OOP Approach**

### **❌ Procedural Approach (C-style)**

```cpp
#include <iostream>
using namespace std;

// Global variables (no encapsulation)
string carModel;
int carYear;

void displayCar() {
    cout << "Car Model: " << carModel << endl;
    cout << "Manufacturing Year: " << carYear << endl;
}

int main() {
    carModel = "Tesla Model X";
    carYear = 2022;
    displayCar();
    return 0;
}
```

✅ **Problems in Procedural Approach**

- No **encapsulation** (Anyone can modify global variables).
- No **reusability** (If we want another car, we have to create duplicate functions).

---

### **✅ OOP Approach (Using Classes & Objects)**

```cpp
#include <iostream>
using namespace std;

// Car class (Encapsulation: Data & methods together)
class Car {
public:
    string model;
    int year;

    // Method to display car details
    void displayCar() {
        cout << "Car Model: " << model << endl;
        cout << "Manufacturing Year: " << year << endl;
    }
};

int main() {
    Car car1; // Creating an object of Car class
    car1.model = "Tesla Model X";
    car1.year = 2022;
    
    car1.displayCar(); // Accessing method using object
    return 0;
}
```

✅ **Advantages of OOP Approach:**  
✔ **Encapsulation:** Data is grouped inside `Car` class.  
✔ **Reusability:** We can create **multiple car objects** without duplicating code.  
✔ **Better Structure:** Code is easier to **read, modify, and extend**.

---
