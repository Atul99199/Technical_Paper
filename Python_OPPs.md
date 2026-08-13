# OOPs in Python with Code Samples

## 1. Introduction

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of **objects**, which contain data and functions that operate on that data.

Python supports OOP and provides features such as:

* Classes and objects
* Encapsulation
* Inheritance
* Polymorphism
* Abstraction
* Constructors
* Method overriding

OOP helps developers write programs that are modular, reusable, maintainable, and easier to understand.

---

## 2. Classes and Objects

A **class** is a blueprint for creating objects. An **object** is an instance of a class.

### Example

```python
class Student:
    def display(self):
        print("I am a student")


student1 = Student()
student1.display()
```

### Output

```text
I am a student
```

Here, `Student` is a class and `student1` is an object of that class.

---

## 3. The `__init__()` Constructor

The `__init__()` method is a special method that is automatically called when an object is created. It is commonly used to initialize object attributes.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student1 = Student("Rahul", 20)
student1.display()
```

### Output

```text
Name: Rahul
Age: 20
```

The `self` parameter refers to the current object.

---

## 4. Encapsulation

**Encapsulation** means combining data and methods within a class and controlling access to the internal data.

Python provides naming conventions for controlling access:

* Public: `name`
* Protected: `_name`
* Private: `__name`

### Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance


account = BankAccount(1000)
account.deposit(500)

print(account.get_balance())
```

### Output

```text
1500
```

The `__balance` attribute is private and should not normally be accessed directly from outside the class.

---

## 5. Inheritance

**Inheritance** allows one class to acquire properties and methods from another class.

The existing class is called the **parent/base class**, while the new class is called the **child/derived class**.

### Example

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


dog = Dog()
dog.eat()
dog.bark()
```

### Output

```text
Animal is eating
Dog is barking
```

The `Dog` class inherits the `eat()` method from `Animal`.

### Types of Inheritance

Python supports several forms of inheritance:

1. Single inheritance
2. Multiple inheritance
3. Multilevel inheritance
4. Hierarchical inheritance
5. Hybrid inheritance

---

## 6. Single Inheritance

In single inheritance, one child class inherits from one parent class.

```python
class Vehicle:
    def start(self):
        print("Vehicle started")


class Car(Vehicle):
    def drive(self):
        print("Car is driving")


car = Car()
car.start()
car.drive()
```

---

## 7. Multiple Inheritance

In multiple inheritance, a child class inherits from more than one parent class.

```python
class Father:
    def skills(self):
        print("Gardening")


class Mother:
    def hobbies(self):
        print("Cooking")


class Child(Father, Mother):
    pass


child = Child()
child.skills()
child.hobbies()
```

### Output

```text
Gardening
Cooking
```

---

## 8. Multilevel Inheritance

In multilevel inheritance, a class inherits from another derived class.

```python
class Grandparent:
    def show_grandparent(self):
        print("Grandparent")


class Parent(Grandparent):
    def show_parent(self):
        print("Parent")


class Child(Parent):
    def show_child(self):
        print("Child")


obj = Child()
obj.show_grandparent()
obj.show_parent()
obj.show_child()
```

---

## 9. Polymorphism

**Polymorphism** means "many forms." In OOP, the same method or interface can behave differently depending on the object using it.

### Method Overriding

A child class can provide its own implementation of a method defined in the parent class.

```python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


class Cat(Animal):
    def sound(self):
        print("Cat meows")


dog = Dog()
cat = Cat()

dog.sound()
cat.sound()
```

### Output

```text
Dog barks
Cat meows
```

The same `sound()` method produces different behavior for different objects.

---

## 10. Polymorphism with a Common Interface

Python's dynamic typing makes polymorphism particularly convenient.

```python
class Dog:
    def speak(self):
        return "Woof!"


class Cat:
    def speak(self):
        return "Meow!"


def animal_speak(animal):
    print(animal.speak())


animal_speak(Dog())
animal_speak(Cat())
```

### Output

```text
Woof!
Meow!
```

The function does not need to know the exact type of object as long as the object provides the required `speak()` method.

---

## 11. Abstraction

**Abstraction** means hiding implementation details and exposing only the essential functionality.

Python provides abstract base classes through the `abc` module.

### Example

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def area(self):
        pass


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius


circle = Circle(5)
print(circle.area())
```

### Output

```text
78.5
```

The `Shape` class defines what a shape must provide, while `Circle` implements the actual calculation.

---

## 12. Class Variables and Instance Variables

An **instance variable** belongs to a particular object, whereas a **class variable** is shared by all objects of the class.

```python
class Student:
    school = "ABC School"

    def __init__(self, name):
        self.name = name


student1 = Student("Amit")
student2 = Student("Priya")

print(student1.name)
print(student2.name)
print(student1.school)
print(student2.school)
```

### Output

```text
Amit
Priya
ABC School
ABC School
```

Here, `name` is an instance variable and `school` is a class variable.

---

## 13. Instance Methods

Instance methods operate on individual objects and normally use `self`.

```python
class Calculator:
    def __init__(self, number):
        self.number = number

    def square(self):
        return self.number ** 2


calculator = Calculator(5)
print(calculator.square())
```

### Output

```text
25
```

---

## 14. Class Methods

A class method operates on the class rather than a particular instance. It uses `cls` and the `@classmethod` decorator.

```python
class Student:
    school = "ABC School"

    def __init__(self, name):
        self.name = name

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school


Student.change_school("XYZ School")

print(Student.school)
```

### Output

```text
XYZ School
```

---

## 15. Static Methods

A static method does not require `self` or `cls`. It is generally used when a method is logically related to a class but does not need class or instance data.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

### Output

```text
30
```

---

## 16. Method Overloading in Python

Traditional method overloading, as found in languages such as Java or C++, is not directly supported in Python.

However, similar behavior can be achieved using default arguments or variable-length arguments.

### Example Using Default Arguments

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c


calculator = Calculator()

print(calculator.add(10))
print(calculator.add(10, 20))
print(calculator.add(10, 20, 30))
```

### Output

```text
10
30
60
```

---

## 17. The `super()` Function

The `super()` function is used to access methods or attributes from a parent class.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed


dog = Dog("Bruno", "Labrador")

print(dog.name)
print(dog.breed)
```

### Output

```text
Bruno
Labrador
```

---

## 18. Magic Methods

Magic methods, also called **dunder methods**, have names beginning and ending with double underscores.

Examples include:

* `__init__()`
* `__str__()`
* `__len__()`
* `__add__()`
* `__eq__()`

### Example with `__str__()`

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name} is {self.age} years old"


student = Student("Anita", 21)

print(student)
```

### Output

```text
Anita is 21 years old
```

---

## 19. Operator Overloading

Python allows operators to be customized using special methods.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"


p1 = Point(2, 3)
p2 = Point(4, 5)

p3 = p1 + p2

print(p3)
```

### Output

```text
(6, 8)
```

The `+` operator is customized using the `__add__()` method.

---

## 20. Advantages of OOP

Object-Oriented Programming provides several advantages:

### 20.1 Reusability

Inheritance allows existing code to be reused in new classes.

### 20.2 Maintainability

Organizing code into classes makes large programs easier to maintain.

### 20.3 Encapsulation

Data and behavior can be grouped together while controlling access to internal implementation details.

### 20.4 Flexibility

Polymorphism allows different objects to be used through a common interface.

### 20.5 Scalability

OOP makes it easier to extend applications as their requirements grow.

---

## 21. Real-World Example

The following example combines several OOP concepts.

```python
from abc import ABC, abstractmethod


class Employee(ABC):

    def __init__(self, name, salary):
        self.name = name
        self.__salary = salary

    def get_salary(self):
        return self.__salary

    @abstractmethod
    def calculate_bonus(self):
        pass


class Developer(Employee):

    def calculate_bonus(self):
        return self.get_salary() * 0.10


class Manager(Employee):

    def calculate_bonus(self):
        return self.get_salary() * 0.20


developer = Developer("Rahul", 50000)
manager = Manager("Priya", 80000)

print(developer.name, developer.calculate_bonus())
print(manager.name, manager.calculate_bonus())
```

### Output

```text
Rahul 5000.0
Priya 16000.0
```

This example demonstrates:

* **Encapsulation** through `__salary`
* **Inheritance** through `Developer` and `Manager`
* **Abstraction** through the `Employee` abstract class
* **Polymorphism** through different implementations of `calculate_bonus()`

---

## 22. OOP Concepts at a Glance

| Concept           | Meaning                            | Python Example           |
| ----------------- | ---------------------------------- | ------------------------ |
| Class             | Blueprint for objects              | `class Student:`         |
| Object            | Instance of a class                | `Student()`              |
| Encapsulation     | Bundling and controlling data      | `__salary`               |
| Inheritance       | Reusing parent-class functionality | `class Dog(Animal)`      |
| Polymorphism      | Same interface, different behavior | `sound()`                |
| Abstraction       | Hiding implementation details      | `ABC`, `@abstractmethod` |
| Constructor       | Initializes an object              | `__init__()`             |
| Method overriding | Child changes parent behavior      | Redefining `sound()`     |

---

## 23. Conclusion

Object-Oriented Programming is an important programming paradigm in Python. It provides mechanisms for organizing software around objects and their behavior.

The four fundamental principles of OOP are:

1. **Encapsulation** — protecting and organizing data.
2. **Inheritance** — reusing functionality from existing classes.
3. **Polymorphism** — allowing a common interface to have different implementations.
4. **Abstraction** — exposing essential functionality while hiding implementation details.

By understanding these concepts and practicing them with real-world examples, developers can build Python applications that are more reusable, organized, maintainable, and scalable.
