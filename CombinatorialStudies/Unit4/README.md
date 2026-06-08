# Unit 4: Fundamentals of Programming Languages (C/C++/Java/OOP)

---

## 4.1 C Language Specifics

### Valid Variable Names in C:
- Must start with a **letter or underscore** (not digit)
- Can contain letters, digits, underscores
- **Cannot be a keyword** (`int`, `float`, `return`, `true`, etc.)
- Case-sensitive

| Variable | Valid? | Reason |
|---|---|---|
| `int number;` | ✅ | Valid identifier |
| `float rate;` | ✅ | Valid |
| `int variable_count;` | ✅ | Underscore allowed |
| `int $main;` | ❌ | `$` not allowed in standard C |
| `float 1var;` | ❌ | Cannot start with digit |

> **PYQ: Which is NOT a valid C variable name? → `int $main;`** ✅

### Cannot be a variable name in C:
- `true` → **Cannot** (it's a keyword/macro in C99+/stdbool.h)
- `volatile` → Cannot (keyword)
- `friend` → Valid in C (only keyword in C++)
- `export` → Valid in C

> **PYQ: Which cannot be a variable name in C? → `true`** ✅

### Result of Logical/Relational Expression in C:
- Result is always **0 or 1** (integer)
- `0` if expression is **false**
- `1` (or any non-zero) if **true**
- **0 if an expression is false and any positive number if true**

> **PYQ: What is the result of logical or relational expression in C?**  
> **c) 0 if false, and any positive number if true** ✅

### Operator Precedence & Associativity:
- Two operators can have: different precedence + same associativity, same precedence + same associativity, different precedence + different associativity
- **NOT possible: Same precedence, different associativity**

> **PYQ: Which is NOT possible with any 2 operators in C?**  
> **c) Same precedence, different associativity** ✅

### Functions in C:
- Functions in C are always **External** by default (can be called from other files unless declared `static`)

> **PYQ: Functions in C Language are always → b) External** ✅

---

## 4.2 C++ Specifics

### User-Defined Header File Extension:
- C++: `.h` or `.hpp`
- User-defined: `.H` or `.h`

> **PYQ: User-defined header file extension in C++? → c) .H** ✅

### Types of Constructors in C++:
| Type | Description |
|---|---|
| **Default Constructor** | No parameters |
| **Parameterized Constructor** | Takes parameters |
| **Copy Constructor** | Creates copy of existing object |
| **NOT a constructor: Friend Constructor** | ❌ No such thing exists |

> **PYQ: Which is NOT a type of constructor? → d) Friend constructor** ✅

### C++ Approach:
- C++ follows **Bottom-Up** approach (OOP: build small objects → combine into larger systems)
- C follows **Top-Down** approach (Procedural: break big problem → smaller functions)

> **PYQ: Which approach is used by C++? → c) Bottom-up** ✅

### Type Provided by C++ but NOT C:
- `bool` type is native in C++ but NOT in standard C (C99 added `_Bool` via stdbool.h)

> **PYQ: Type provided by C++ but not C? → d) bool** ✅

### Virtual Inheritance in C++:
- Used to solve the **Diamond Problem** in multiple inheritance
- Ensures only **ONE copy** of the base class exists in derived classes
- **Technique to avoid multiple copies of base class into children/derived class**

> **PYQ: Virtual inheritance? → d) C++ technique to avoid multiple copies of the base class into children/derived class** ✅

### Destructor: `~ClassName()` — called when object is destroyed  
### Pure Virtual Function: `virtual void func() = 0;` → makes class abstract

---

## 4.3 Java Specifics

### Key Java Facts:
- Java is a **platform-independent** programming language (Write Once, Run Anywhere — JVM)
- Java does **NOT have pointers** (uses references instead)
- Java does NOT support **multiple inheritance with classes** (uses interfaces)
- Java does NOT support **operator overloading** (except `+` for strings)

> **PYQ: Which is NOT a Java feature? → b) Use of pointers** ✅  
> **PYQ: Which is true about Java? → d) Java is a platform-independent programming language** ✅

### JavaPATH / JAVA_HOME:
- Environment variable to set Java path: **JAVA_HOME**

> **PYQ: Which environment variable sets Java path? → d) JAVA_HOME** ✅

### `this` keyword in Java:
- Refers to **current object**
- Used for: (1) Referring to instance variable when local has same name, (2) Passing itself to another method, (3) Calling another constructor (constructor chaining)
- **NOT for:** Passing itself to a method of the same class (it's used for calling method, not passing)

> **PYQ: What is NOT a use of `this`? → b) Passing itself to the method of the same class** ✅

### Polymorphism Types in Java:
| Type | Also Called | How |
|---|---|---|
| **Compile-time** | Static / Early binding | Method Overloading |
| **Runtime** | Dynamic / Late binding | Method Overriding |

> **PYQ: Types of polymorphism? → b) Compile time polymorphism and d) Execution time polymorphism** ✅

---

## 4.4 OOP Concepts

### Four Pillars:
| Pillar | Definition |
|---|---|
| **Encapsulation** | Bundle data + methods; hide data (private) |
| **Abstraction** | Hide complexity; show essentials (abstract class, interface) |
| **Inheritance** | Child acquires parent's properties; code reuse |
| **Polymorphism** | Same name, different behavior |

### Inheritance Types:
| Type | Description |
|---|---|
| Single | A → B |
| Multilevel | A → B → C |
| Hierarchical | A → B, A → C |
| Multiple | B, C → D (C++ only, NOT Java classes) |
| Hybrid | Combination |

### Overloading vs Overriding:
| Feature | Overloading | Overriding |
|---|---|---|
| Parameters | Different | Same |
| Class | Same class | Parent-child |
| Binding | Compile-time | Runtime |

### Access Modifiers:
| Modifier | Same Class | Package | Subclass | World |
|---|---|---|---|---|
| private | ✅ | ❌ | ❌ | ❌ |
| default | ✅ | ✅ | ❌ | ❌ |
| protected | ✅ | ✅ | ✅ | ❌ |
| public | ✅ | ✅ | ✅ | ✅ |

### Abstract Class vs Interface:
| Feature | Abstract Class | Interface |
|---|---|---|
| Methods | Abstract + concrete | All abstract (Java 8+: default) |
| Variables | Any | public static final only |
| Extend | Single | Multiple |

---

## 4.5 Pointers (C/C++)

```c
int x = 10;
int *ptr = &x;     // ptr stores address of x
printf("%d", *ptr); // Dereference → prints 10
```

| Type | Description |
|---|---|
| **NULL pointer** | Points to nothing (0) |
| **Dangling pointer** | Points to freed memory |
| **Wild pointer** | Uninitialized |
| **Void pointer** | `void*` — generic, any type |

### Storage Classes:
| Class | Scope | Lifetime | Default |
|---|---|---|---|
| **auto** | Local | Block | Garbage |
| **register** | Local | Block | Garbage |
| **static** | Local (persists) | Entire program | 0 |
| **extern** | Global (across files) | Entire program | 0 |

---

## 4.6 Parameter Passing & Memory

| Method | Original Changed? |
|---|---|
| **Pass by Value** | No (copy) |
| **Pass by Reference** (&) | Yes |
| **Pass by Pointer** (*) | Yes |

### Memory:
| Area | Stores |
|---|---|
| **Stack** | Local vars, function calls (automatic, LIFO) |
| **Heap** | Dynamic allocation (malloc/new) |
| **Code** | Program instructions |
| **Data** | Global/static variables |

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** Which is NOT a valid C variable name?

a) int number;  
b) float rate;  
c) int variable_count;  
**d) int $main; ✅**

---

**Q2.** Which cannot be a variable name in C?

a) volatile  
**b) true ✅**  
c) friend  
d) export

---

**Q3.** Result of logical or relational expression in C?

a) True or False  
b) 0 or 1  
**c) 0 if false and any positive number if true ✅**  
d) None

---

**Q4.** Which is NOT possible with any 2 operators in C?

a) Different precedence, same associativity  
b) Different precedence, different associativity  
**c) Same precedence, different associativity ✅**  
d) All of the mentioned

---

**Q5.** Functions in C Language are always:

a) Internal  
**b) External ✅**  
c) Both  
d) Neither

---

**Q6.** User-defined header file extension in C++?

a) .Hg  
b) .Cpp  
**c) .H ✅**  
d) .Hf

---

**Q7.** Which is NOT a type of constructor in C++?

a) Default constructor  
b) Parameterized constructor  
c) Copy constructor  
**d) Friend constructor ✅**

---

**Q8.** C++ uses which approach?

a) Left-right  
b) Right-left  
**c) Bottom-up ✅**  
d) Top-down

---

**Q9.** Type provided by C++ but NOT C?

a) double  
b) float  
c) int  
**d) bool ✅**

---

**Q10.** Virtual inheritance in C++ is:

a) Enhance multiple inheritance  
b) Access private members  
c) Avoid multiple inheritances  
**d) Avoid multiple copies of base class in derived class ✅**

---

**Q11.** Which is true about Java?

a) Sequence-dependent  
b) Code dependent  
c) Platform-dependent  
**d) Platform-independent ✅**

---

**Q12.** Which is NOT a Java feature?

a) Object-oriented  
**b) Use of pointers ✅**  
c) Portable  
d) Dynamic and Extensible

---

**Q13.** Environment variable to set Java path?

a) MAVEN_Path  
b) JavaPATH  
c) JAVA  
**d) JAVA_HOME ✅**

---

**Q14.** What is NOT a use of `this` keyword in Java?

a) Referring to instance variable  
**b) Passing itself to method of same class ✅**  
c) Passing itself to another method  
d) Calling another constructor

---

**Q15.** Types of polymorphism in Java:

a) Multiple polymorphism  
**b) Compile time polymorphism ✅**  
c) Multilevel polymorphism  
**d) Execution time polymorphism ✅**

---

**Q16.** Encapsulation hides data using:

**a) Access modifiers (private) ✅**  
b) Abstract class  
c) Inheritance  
d) Polymorphism

---

**Q17.** Method overloading is:

**a) Compile-time polymorphism ✅**  
b) Runtime polymorphism  
c) Inheritance  
d) Encapsulation

---

**Q18.** Method overriding is:

a) Compile-time  
**b) Runtime polymorphism ✅**  
c) Encapsulation  
d) Abstraction

---

**Q19.** Java does NOT support:

a) Single inheritance  
**b) Multiple inheritance with classes ✅**  
c) Interfaces  
d) Encapsulation

---

**Q20.** `final` in Java prevents class from being:

**a) Inherited ✅**  
b) Instantiated  
c) Compiled  
d) Loaded

---

**Q21.** A pointer stores:

a) Value  
**b) Memory address ✅**  
c) File path  
d) Function

---

**Q22.** Dangling pointer points to:

a) NULL  
**b) Freed memory ✅**  
c) Valid variable  
d) Stack

---

**Q23.** Constructor is called:

**a) Automatically when object is created ✅**  
b) Manually  
c) At program end  
d) Never

---

**Q24.** Most restrictive access modifier:

**a) private ✅**  
b) protected  
c) public  
d) default

---

**Q25.** Abstract class CAN have:

**a) Both abstract and concrete methods ✅**  
b) Only abstract  
c) Only static  
d) No methods

---

**Q26.** `super` refers to:

**a) Parent class ✅**  
b) Current object  
c) Static variable  
d) Interface

---

**Q27.** `static` member retains value:

a) Until block ends  
**b) Entire program lifetime ✅**  
c) One function call  
d) Never

---

**Q28.** Default storage class in C:

**a) auto ✅**  
b) static  
c) extern  
d) register

---

**Q29.** Pass by value:

**a) Copy passed; original NOT changed ✅**  
b) Address passed  
c) Original changed  
d) Both changed

---

**Q30.** malloc() allocates on:

a) Stack  
**b) Heap ✅**  
c) Code  
d) Register

---

**Q31.** Local variables are on:

**a) Stack ✅**  
b) Heap  
c) Data segment  
d) Code

---

**Q32.** Java garbage collector frees:

**a) Unreferenced objects on heap ✅**  
b) Stack  
c) Code  
d) All

---

**Q33.** Diamond Problem occurs in:

**a) Multiple inheritance ✅**  
b) Single  
c) Encapsulation  
d) Abstraction

---

**Q34.** OOP concept that promotes code reuse:

**a) Inheritance ✅**  
b) Encapsulation  
c) Abstraction  
d) Polymorphism

---

**Q35.** NULL pointer value:

**a) 0 ✅**  
b) -1  
c) 1  
d) Undefined

---

**Q36.** `new` in C++:

a) Only allocates memory  
**b) Allocates memory AND calls constructor ✅**  
c) Only calls constructor  
d) Frees memory

---

**Q37.** Stack overflow caused by:

**a) Infinite recursion ✅**  
b) Memory leak  
c) NULL pointer  
d) Too many variables

---

**Q38.** Memory leak:

**a) Allocated memory never freed ✅**  
b) Memory freed twice  
c) Stack overflow  
d) Segfault

---

**Q39.** Abstraction achieved by:

**a) Abstract classes and interfaces ✅**  
b) Loops  
c) Arrays  
d) Pointers

---

**Q40.** Overloading requires:

**a) Different parameters (type/number/order) ✅**  
b) Same parameters  
c) Different class  
d) Same return type

---

**Q41.** Overriding requires:

**a) Same method signature in parent-child ✅**  
b) Different parameters  
c) Same class  
d) Static methods

---

**Q42.** A → B → C is which inheritance?

a) Single  
**b) Multilevel ✅**  
c) Multiple  
d) Hierarchical

---

**Q43.** Multiple children from one parent:

**a) Hierarchical ✅**  
b) Single  
c) Multilevel  
d) Multiple

---

**Q44.** Static method belongs to:

**a) Class ✅**  
b) Object  
c) Constructor  
d) Destructor

---

**Q45.** Destructor in C++ starts with:

**a) ~ (tilde) ✅**  
b) #  
c) @  
d) !

---

**Q46.** `sizeof` returns:

**a) Size in bytes ✅**  
b) Value  
c) Address  
d) Type

---

**Q47.** `final` variable in Java:

**a) Constant — value cannot change ✅**  
b) Always 0  
c) Private  
d) Static

---

**Q48.** Pure virtual function in C++:

**a) `virtual void func() = 0;` ✅**  
b) `virtual void func() {}`  
c) `abstract void func();`  
d) `void func() = 0;`

---

**Q49.** `extern` allows variable across:

**a) Multiple files ✅**  
b) One function  
c) One block  
d) Main only

---

**Q50.** Shallow copy copies:

**a) Only references/pointers (not pointed data) ✅**  
b) Everything deeply  
c) Nothing  
d) Only primitives

---

## Scenario / One-Line Answers

**S1.** `$main` invalid in C because `$` is not allowed in standard C variable names.  
**S2.** `true` cannot be variable in C because it's defined as a macro in `<stdbool.h>` (C99+).  
**S3.** C logical expressions always return 0 (false) or non-zero positive (true).  
**S4.** Same precedence, different associativity is impossible for any 2 C operators.  
**S5.** C functions default to external linkage (accessible from other files unless declared `static`).  
**S6.** Virtual inheritance = one copy of base class in diamond hierarchy.  
**S7.** Java is platform-independent because it compiles to bytecode executed by JVM.  
**S8.** Java has no pointers — it uses references (no pointer arithmetic possible).  
**S9.** `bool` is native in C++ but not in C (C99 added `_Bool`).  
**S10.** Bottom-up = OOP approach (C++); Top-down = Procedural (C).

---
