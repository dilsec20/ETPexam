# Unit 4: Fundamentals of Programming Languages (OOP)

---

## 4.1 C/C++/Java Concepts

### Pointers (C/C++)
A **pointer** is a variable that stores the **memory address** of another variable.

```c
int x = 10;
int *ptr = &x;   // ptr stores address of x
printf("%d", *ptr); // Dereference: prints 10
```

| Concept | Description |
|---|---|
| **&** (Address-of) | Returns the address of a variable |
| **\*** (Dereference) | Accesses the value at the address |
| **NULL pointer** | Pointer that points to nothing (address 0) |
| **Dangling pointer** | Pointer that refers to memory that has been freed |
| **Wild pointer** | Uninitialized pointer; points to random memory |
| **Void pointer** | Generic pointer (`void *`) that can point to any data type |
| **Pointer arithmetic** | Incrementing a pointer moves it by the size of the data type |

### Storage Classes (C/C++):
| Class | Scope | Lifetime | Default Value |
|---|---|---|---|
| **auto** | Local (block) | Until block ends | Garbage |
| **register** | Local | Until block ends | Garbage |
| **static** | Local (but persists) | Entire program | 0 |
| **extern** | Global (across files) | Entire program | 0 |

---

## 4.2 Object-Oriented Programming (OOP)

### Four Pillars of OOP:

| Pillar | Definition |
|---|---|
| **Encapsulation** | Bundling data (variables) and methods (functions) that operate on that data into a single unit (class). Data is hidden using access modifiers (private). |
| **Abstraction** | Hiding complex implementation details and showing only essential features. Achieved using abstract classes and interfaces. |
| **Inheritance** | A class (child) acquires properties and methods of another class (parent). Promotes code reuse. |
| **Polymorphism** | Same name, different behavior. One interface, multiple implementations. |

### Types of Inheritance:
| Type | Description |
|---|---|
| **Single** | One child inherits from one parent |
| **Multilevel** | A → B → C (chain) |
| **Hierarchical** | Multiple children inherit from one parent |
| **Multiple** | One child inherits from multiple parents (C++ only, NOT Java) |
| **Hybrid** | Combination of two or more types |

> **Java does NOT support multiple inheritance with classes** (to avoid the Diamond Problem). It supports it through **interfaces**.

### Diamond Problem:
When a class inherits from two classes that have a common parent, ambiguity arises about which parent's method to use. Solved in C++ using **virtual inheritance**.

### Polymorphism Types:
| Type | Also Called | How |
|---|---|---|
| **Compile-time** | Static / Early Binding | Method Overloading, Operator Overloading |
| **Runtime** | Dynamic / Late Binding | Method Overriding (using virtual functions / inheritance) |

### Overloading vs Overriding:
| Feature | Overloading | Overriding |
|---|---|---|
| Same name | Yes | Yes |
| Same parameters | No (different) | Yes (same) |
| Same class | Yes | No (parent-child) |
| Binding | Compile-time | Runtime |
| Return type | Can differ | Must be same (or covariant) |

### Access Modifiers:
| Modifier | Same Class | Same Package | Subclass | World |
|---|---|---|---|---|
| **private** | ✅ | ❌ | ❌ | ❌ |
| **default** | ✅ | ✅ | ❌ | ❌ |
| **protected** | ✅ | ✅ | ✅ | ❌ |
| **public** | ✅ | ✅ | ✅ | ✅ |

---

## 4.3 Classes & Objects

| Concept | Definition |
|---|---|
| **Class** | Blueprint/template for creating objects. Defines attributes and methods. |
| **Object** | Instance of a class. Has state (attributes) and behavior (methods). |
| **Constructor** | Special method that initializes an object. Same name as class. Called automatically. |
| **Destructor** | Method called when object is destroyed (C++: `~ClassName()`). Java uses garbage collector. |
| **this keyword** | Reference to the current object |
| **static** | Belongs to the class, not to any specific object. Shared among all objects. |
| **final (Java)** | Variable: constant. Method: cannot be overridden. Class: cannot be inherited. |
| **abstract class** | Cannot be instantiated. Can have abstract (no body) and concrete methods. |
| **interface** | 100% abstract (all methods abstract). Defines a contract. A class "implements" an interface. |

### Abstract Class vs Interface:
| Feature | Abstract Class | Interface |
|---|---|---|
| Methods | Both abstract and concrete | All abstract (Java 8+: default methods too) |
| Variables | Any type | Only public static final |
| Inheritance | extends (single) | implements (multiple) |
| Constructor | Yes | No |

---

## 4.4 Parameter Passing

| Method | Description | Language |
|---|---|---|
| **Pass by Value** | Copy of the value is passed. Original not modified. | C, Java (primitives) |
| **Pass by Reference** | Reference (address) is passed. Original IS modified. | C++ (&), Java (objects) |
| **Pass by Pointer** | Pointer (address) is passed explicitly. | C, C++ |

```c
// Pass by Value — original NOT changed
void change(int x) { x = 100; }
int a = 5;
change(a);  // a is still 5

// Pass by Reference (C++) — original CHANGED
void change(int &x) { x = 100; }
int a = 5;
change(a);  // a is now 100

// Pass by Pointer — original CHANGED
void change(int *x) { *x = 100; }
int a = 5;
change(&a);  // a is now 100
```

> **Java:** Primitives are pass by value. Objects are pass by reference of the reference (you can modify object's fields, but reassigning the reference doesn't affect the original).

---

## 4.5 Memory Handling

| Memory Area | What's Stored | Allocation |
|---|---|---|
| **Stack** | Local variables, function calls, return addresses | Automatic (LIFO) |
| **Heap** | Dynamically allocated memory (new, malloc) | Manual (or garbage collected) |
| **Code/Text** | Program instructions | Fixed |
| **Data (BSS + Global)** | Global/static variables | Fixed |

### C/C++ Memory:
```c
// malloc — allocates memory, returns void*
int *arr = (int*) malloc(5 * sizeof(int));
free(arr);  // Must free manually

// new (C++) — allocates and calls constructor
int *p = new int(10);
delete p;   // Must delete manually

// Memory Leak: Forgetting to free/delete allocated memory
```

### Java Memory:
```java
// Objects created on heap using 'new'
String s = new String("Hello");
// Java has Garbage Collector — automatically frees unused objects
// No need for free() or delete
```

### Garbage Collection:
Automatic memory management in Java/C#/Python. The GC identifies and frees objects that are no longer referenced. Key algorithms: Mark-and-Sweep, Generational GC.

### Common Memory Issues:
| Issue | Description |
|---|---|
| **Memory Leak** | Allocated memory never freed → program uses more and more memory |
| **Dangling Pointer** | Pointer to freed memory → undefined behavior |
| **Buffer Overflow** | Writing beyond allocated memory → security vulnerability |
| **Stack Overflow** | Infinite recursion or too many function calls exhausts stack |
| **Segmentation Fault** | Accessing memory that doesn't belong to the program |

---

## MCQ Practice Questions (50+)

---

**Q1.** Which OOP pillar hides data using access modifiers?
**A. Encapsulation ✅**  B. Abstraction  C. Inheritance  D. Polymorphism

---

**Q2.** Method overloading is an example of:
**A. Compile-time polymorphism ✅**  B. Runtime polymorphism  C. Inheritance  D. Encapsulation

---

**Q3.** Method overriding is an example of:
A. Compile-time polymorphism  **B. Runtime polymorphism ✅**  C. Encapsulation  D. Abstraction

---

**Q4.** Java does NOT support:
A. Single inheritance  **B. Multiple inheritance with classes ✅**  C. Interfaces  D. Encapsulation

---

**Q5.** Which keyword prevents a class from being inherited in Java?
A. static  B. abstract  **C. final ✅**  D. private

---

**Q6.** A pointer stores:
A. A value  **B. A memory address ✅**  C. A file path  D. A function

---

**Q7.** A dangling pointer points to:
A. NULL  B. A valid variable  **C. Memory that has been freed ✅**  D. The stack

---

**Q8.** Constructor is called:
A. Manually  **B. Automatically when an object is created ✅**  C. At program end  D. Never

---

**Q9.** Which access modifier is most restrictive?
**A. private ✅**  B. protected  C. public  D. default

---

**Q10.** Abstract class CAN have:
A. Only abstract methods  **B. Both abstract and concrete methods ✅**  C. Only static methods  D. No methods

---

**Q11.** An interface in Java can contain:
A. Instance variables  **B. Only public static final variables and abstract methods ✅**  C. Constructors  D. Private methods

---

**Q12.** `this` keyword refers to:
A. Parent class  **B. Current object ✅**  C. Static method  D. Main method

---

**Q13.** `super` keyword refers to:
**A. Parent class ✅**  B. Current object  C. Static variable  D. Interface

---

**Q14.** Which storage class retains value between function calls?
A. auto  B. register  **C. static ✅**  D. extern

---

**Q15.** Default storage class in C:
**A. auto ✅**  B. static  C. extern  D. register

---

**Q16.** Pass by value means:
**A. Copy of value is passed; original not changed ✅**  B. Address is passed  C. Original is changed  D. Both are changed

---

**Q17.** In C++, pass by reference uses:
A. * operator  **B. & operator ✅**  C. -> operator  D. . operator

---

**Q18.** Memory allocated using malloc() is on:
A. Stack  **B. Heap ✅**  C. Code segment  D. Register

---

**Q19.** Local variables are stored on:
**A. Stack ✅**  B. Heap  C. Data segment  D. Code segment

---

**Q20.** Java garbage collector frees:
A. Stack memory  **B. Heap memory (unreferenced objects) ✅**  C. Code memory  D. All memory

---

**Q21.** Diamond Problem occurs in:
A. Single inheritance  **B. Multiple inheritance ✅**  C. Encapsulation  D. Abstraction

---

**Q22.** Polymorphism means:
A. One class, one method  **B. Same name, different behavior ✅**  C. Hiding data  D. Copying classes

---

**Q23.** Which OOP concept promotes code reuse?
A. Encapsulation  B. Abstraction  **C. Inheritance ✅**  D. Polymorphism

---

**Q24.** A NULL pointer in C has the value:
A. -1  **B. 0 ✅**  C. 1  D. Undefined

---

**Q25.** `void*` is called a:
A. Null pointer  **B. Void/Generic pointer ✅**  C. Dangling pointer  D. Wild pointer

---

**Q26.** Which function allocates memory in C?
**A. malloc() ✅**  B. alloc()  C. new  D. create()

---

**Q27.** Which function frees memory in C?
A. delete  **B. free() ✅**  C. remove()  D. dispose()

---

**Q28.** In C++, `new` keyword does:
A. Only allocates memory  **B. Allocates memory AND calls constructor ✅**  C. Only calls constructor  D. Frees memory

---

**Q29.** Stack overflow is caused by:
A. Too many variables  **B. Infinite recursion ✅**  C. Memory leak  D. NULL pointer

---

**Q30.** Buffer overflow is a _____ vulnerability:
**A. Security ✅**  B. Performance  C. Logic  D. Syntax

---

**Q31.** Memory leak occurs when:
**A. Allocated memory is never freed ✅**  B. Memory is freed twice  C. Stack overflows  D. Too many variables

---

**Q32.** Abstraction is achieved in Java using:
A. Encapsulation  **B. Abstract classes and interfaces ✅**  C. Loops  D. Arrays

---

**Q33.** In Java, all objects are created on:
A. Stack  **B. Heap ✅**  C. Code segment  D. Register

---

**Q34.** A class that cannot be instantiated is:
**A. Abstract class ✅**  B. Final class  C. Static class  D. Inner class

---

**Q35.** Overloading requires:
A. Same parameters  **B. Different parameters (type, number, or order) ✅**  C. Different class  D. Same return type

---

**Q36.** Overriding requires:
**A. Same method signature in parent and child class ✅**  B. Different parameters  C. Same class  D. Static methods

---

**Q37.** Which type of inheritance is: A → B → C?
A. Single  **B. Multilevel ✅**  C. Multiple  D. Hierarchical

---

**Q38.** Which type: Multiple children from one parent?
A. Single  B. Multilevel  C. Multiple  **D. Hierarchical ✅**

---

**Q39.** Static method belongs to:
A. Object  **B. Class ✅**  C. Constructor  D. Destructor

---

**Q40.** Destructor in C++ starts with:
**A. ~ (tilde) ✅**  B. #  C. @  D. !

---

**Q41.** Java primitives (int, char, float) are passed by:
**A. Value ✅**  B. Reference  C. Pointer  D. Name

---

**Q42.** `sizeof` operator in C returns:
A. Value of variable  **B. Size in bytes ✅**  C. Address  D. Type

---

**Q43.** Which concept allows different classes to be treated through the same interface?
A. Encapsulation  B. Abstraction  C. Inheritance  **D. Polymorphism ✅**

---

**Q44.** `final` variable in Java is:
**A. A constant — its value cannot change ✅**  B. Always 0  C. Private  D. Static

---

**Q45.** Virtual function in C++ enables:
A. Compile-time binding  **B. Runtime polymorphism ✅**  C. Multiple inheritance  D. Encapsulation

---

**Q46.** Pure virtual function syntax in C++:
A. `virtual void func() {}`  **B. `virtual void func() = 0;` ✅**  C. `abstract void func();`  D. `void func() = 0;`

---

**Q47.** A class with at least one pure virtual function is:
**A. Abstract class ✅**  B. Final class  C. Static class  D. Concrete class

---

**Q48.** `extern` storage class allows a variable to be used:
A. Only in one function  **B. Across multiple files ✅**  C. Only in main  D. Only in loops

---

**Q49.** Copy constructor creates:
**A. A new object as a copy of an existing object ✅**  B. A pointer  C. A static object  D. A destructor

---

**Q50.** Shallow copy copies:
A. All data deeply  **B. Only references/pointers (not the pointed data) ✅**  C. Nothing  D. Only primitives

---

## Scenario & One-Line Answer Questions

---

**S1.** What is the difference between a class and an object?
> A **class** is a blueprint/template. An **object** is an instance of a class with actual values.

**S2.** Can a constructor be private? When would you use it?
> Yes. Private constructor is used in the **Singleton design pattern** — to ensure only one instance of a class exists.

**S3.** What is the difference between an abstract class and an interface?
> Abstract class can have both abstract and concrete methods, constructors, and any variables. Interface (traditionally) has only abstract methods and constants. A class can implement multiple interfaces but extend only one abstract class.

**S4.** What is the difference between `==` and `.equals()` in Java?
> `==` compares **references** (memory addresses). `.equals()` compares **values** (content). For strings: `"abc" == "abc"` may be true (string pool), but use `.equals()` for reliable comparison.

**S5.** What is early binding vs late binding?
> **Early binding** (compile-time): method call resolved at compile time (overloading). **Late binding** (runtime): resolved at runtime using actual object type (overriding, virtual functions).

**S6.** What happens if you forget to free memory allocated with malloc()?
> **Memory leak** — the program continues to use more memory over time because the allocated block is never returned to the system.

**S7.** What is the difference between stack and heap memory?
> **Stack**: automatic, fast, LIFO, stores local variables. **Heap**: manual allocation (malloc/new), slower, stores dynamic data, must be freed manually (or by GC).

**S8.** Can we overload the main() method in Java?
> Yes, but the JVM always calls `public static void main(String[] args)`. Other overloaded versions can be called manually.

**S9.** What is the difference between shallow copy and deep copy?
> **Shallow copy** copies references — both original and copy point to the same data. **Deep copy** creates completely new copies of all referenced data.

**S10.** What is a friend function in C++?
> A function declared with `friend` keyword inside a class that can access private and protected members of that class, even though it's not a member.

---
