
# 📌 **2️⃣ Classes & Objects**

## ✅ **What is a Class?**

A **Class** is a blueprint for creating **Objects**. It defines **attributes (variables)** and **methods (functions)** related to an entity.

### **✅ What is an Object?**

An **Object** is an **instance** of a class. It represents a real-world entity with properties (data members) and behavior (methods).

---

## ✅ **Defining a Class in C++**

```cpp
#include <iostream>
using namespace std;

// Defining a class named 'Person'
class Person {
public:
    // Data members (Attributes)
    string name;
    int age;

    // Member function (Method)
    void introduce() {
        cout << "Hello, my name is " << name << " and I am " << age << " years old." << endl;
    }
};

int main() {
    // Creating an object of Person class
    Person person1;
    person1.name = "John Doe";
    person1.age = 25;

    // Calling a method using the object
    person1.introduce();
    return 0;
}
```

✅ **Explanation:**

- **`class Person`**: Defines a **blueprint** for a person.
- **`name` & `age`**: Data members (variables storing person's info).
- **`introduce()`**: Member function (prints introduction).
- **`Person person1;`**: Creates an **object (instance)** of `Person`.

**💡 Output:**

```
Hello, my name is John Doe and I am 25 years old.
```

---

## ✅ **Accessing Members of a Class**

By default, **class members** in C++ are **private** (not accessible from outside the class).  
To access them, we use the **public** access modifier.

### **Example: Accessing Members Using Public Modifier**

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    string species;

    // Method to set species name
    void setSpecies(string s) {
        species = s;
    }

    // Method to display species
    void getSpecies() {
        cout << "The species is: " << species << endl;
    }
};

int main() {
    Animal animal1;
    animal1.setSpecies("Lion");
    animal1.getSpecies();
    return 0;
}
```

✅ **Explanation:**

- **`public` modifier** makes `species` accessible from outside the class.
- **Methods `setSpecies()` & `getSpecies()`** are used to modify and retrieve data.

**💡 Output:**

```
The species is: Lion
```

---

# **📖 Layman’s Section – Understanding Classes & Objects Easily**

|**Concept**|**Real-Life Example**|
|---|---|
|**Class**|A **blueprint** for a house|
|**Object**|An **actual house** built from the blueprint|
|**Attributes (Data Members)**|The **color, size, and rooms** of the house|
|**Methods (Functions)**|Actions the house can perform (e.g., **open door, turn on lights**)|

### **💡 Example Analogy:**

Imagine you want to **build a car factory**.

- The **blueprint (Class)** defines the car's **shape, engine, color, features**.
- Each **car (Object)** is created based on the blueprint.
- Each car has **its own unique values** (color, model, year).

---

# 🎯 **Final Summary**

✅ **OOP organizes code using objects and classes** to model real-world entities.  
✅ **Classes** act as **blueprints**, and **objects** are instances of those classes.  
✅ **Encapsulation groups data and methods together** to improve security and organization.

🚀 **Next Steps:**  
Let me know if you want to dive into **Encapsulation & Abstraction** with examples! 😊