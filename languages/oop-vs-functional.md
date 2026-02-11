# Object Oriented Programming vs Functional Programming

Object Oriented Programming (OOP) and Functional Programming (FP) are two dominant paradigms in software development.

- OOP: Organizes software around "objects" that combine "state" (data) and "methods" (behavior). It is built on four fundamental principles that all CS majors learn in programming 101:
  - Encapsulation
  - Inheritance
  - Polymorphism
  - Abstraction
- FP: Treats computation as functions and avoids changing state and mutable data. It is built around these 4 core concepts:
  - Pure functions - functions always produce the same output
  - Immutability - data structures cannot be modified after creation
  - First-class funcitons - Functions are treated as values that can be passed around
  - Declaritive style - Code expresses what should be computed rather than how to compute

Essentially, OOP treates the world as interacting objects and FP treats it as data transformations. OOP is more intuitive and accessible, but FP is more predictable and composable.

## Key differences
| Aspect | OOP | FP |
| --- | --- | --- |
| State | Mutable states within objects | Immutable data structures |
| Primary building blocks | Objects (data + methods) | Pure functions | 
| Code organization | Class inheritance | Function composition |
| Control flow | Loops, conditionals | Recursion, higher-order functions |
| Concurrency | Requires locks and sync | Safe due to immutability |
| Data and behavior | Tightly coupled in objects | Separated |

## Pros and Cons
OOP excels in UI development (mapping objects with state and behavior), connection pools (many state transitions), and user models (when objects are like real-world metaphors).

FP excels at concurrent distributed systems (race conditions, deadlocks, data corruption handling), ETL processes (map-filter-redce pattern), stateless services, and pricing/validation logic & calculation algorithms (same inputs -> same outputs).

## Compromise
Learn to use both and choose a language that can handle both.

Functional core with imperative shell: Keep business logic pure and functional. Handle I/O, state management, and side effects in a thin layer of objects.

Use immutable data structures even in OOP.

E.g. a microservice that uses functional business logic but OOP for DB connections, HTTP clients, and message queues.