# Technical Paper: Object-Oriented Programming (OOP) in Python
## 1. Introduction
Object-Oriented Programming (OOP) is a programming approach based on classes and objects.
Python supports OOP and provides features that make programs easier to organize, reuse, and maintain.
The main OOP concepts are classes, objects, encapsulation, inheritance, polymorphism, and abstraction.
## 2. Classes and Objects
A class is a blueprint for creating objects.
An object is an instance of a class.
```python
class Student:
    def display(self):
        print("I am a student")
student = Student()
student.display()
```
Here, `Student` is the class and `student` is the object.
## 3. Constructor
The `__init__()` method runs automatically when an object is created.
It is mainly used to initialize object data.
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def display(self):
        print(self.name, self.age)
student = Student("Rahul", 20)
student.display()
```
`self` refers to the current object.
## 4. Encapsulation
Encapsulation means keeping data and methods together inside a class.
It also helps control access to data.
Python commonly uses public, protected, and private naming conventions.
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
Here, `__balance` is treated as private data.
## 5. Inheritance
Inheritance allows one class to reuse methods and properties of another class.
The existing class is the parent class and the new class is the child class.
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
### Types of Inheritance
- Single inheritance
- Multiple inheritance
- Multilevel inheritance
- Hierarchical inheritance
- Hybrid inheritance
One child class inherits from one parent class.
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
One child class inherits from more than one parent class.
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
Inheritance happens through multiple levels.
```python
class Grandparent:
    def show(self):
        print("Grandparent")
class Parent(Grandparent):
    def show_parent(self):
        print("Parent")
class Child(Parent):
    def show_child(self):
        print("Child")
child = Child()
child.show()
child.show_parent()
child.show_child()
```
## 9. Polymorphism
Polymorphism means "many forms."
It allows the same method to behave differently for different objects.
```python
class Animal:
    def sound(self):
        print("Animal sound")
class Dog(Animal):
    def sound(self):
        print("Dog barks")
class Cat(Animal):
    def sound(self):
        print("Cat meows")
Dog().sound()
Cat().sound()
```
## 10. Abstraction
Abstraction means hiding unnecessary implementation details.
Python provides abstract classes using the `abc` module.
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
        return 3.14 * self.radius ** 2
circle = Circle(5)
print(circle.area())
```
`Shape` defines the required method and `Circle` provides its implementation.
## 11. Class and Instance Variables
An instance variable belongs to one object.
A class variable is shared by all objects.
```python
class Student:
    school = "ABC School"
    def __init__(self, name):
        self.name = name
student1 = Student("Amit")
student2 = Student("Priya")
print(student1.name)
print(student1.school)
```
```python
class Calculator:
    def __init__(self, number):
        self.number = number
    def square(self):
        return self.number ** 2
calc = Calculator(5)
print(calc.square())
```
```python
class Student:
    school = "ABC School"
    @classmethod
    def change_school(cls, name):
        cls.school = name
Student.change_school("XYZ School")
print(Student.school)
```
```python
class Calculator:
    @staticmethod
    def add(a, b):
        return a + b
print(Calculator.add(10, 20))
```
## 15. Method Overloading
Python does not directly support traditional method overloading.
Default arguments can be used for similar behavior.
```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c
calc = Calculator()
print(calc.add(10))
print(calc.add(10, 20))
print(calc.add(10, 20, 30))
```
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
Common examples:
- `__init__()` – initializes an object
- `__str__()` – controls object display
- `__len__()` – defines length
- `__add__()` – defines addition
- `__eq__()` – checks equality
### Example
```python
class Student:
    def __init__(self, name):
        self.name = name
    def __str__(self):
        return self.name
student = Student("Anita")
print(student)
```
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
print(p1 + p2)
```
Output:
```text
(6, 8)
```
## 19. Advantages of OOP
OOP provides several benefits:
- **Reusability:** Existing code can be reused.
- **Maintainability:** Code is easier to organize and update.
- **Encapsulation:** Data can be kept protected.
- **Flexibility:** Different objects can have different behaviors.
- **Scalability:** Programs can be extended more easily.
- **Organization:** Large programs can be divided into smaller classes.
## 20. Real-World Example
This example combines inheritance, encapsulation, abstraction, and polymorphism.
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
print(developer.calculate_bonus())
print(manager.calculate_bonus())
```
This example shows:
- Encapsulation through `__salary`
- Inheritance through `Developer` and `Manager`
- Abstraction through `Employee`
- Polymorphism through `calculate_bonus()`
## 21. OOP Concepts at a Glance
| Concept | Simple Meaning |
|---|---|
| Class | Blueprint for objects |
| Object | Instance of a class |
| Encapsulation | Protecting and organizing data |
| Inheritance | Reusing code from a parent |
| Polymorphism | Same method, different behavior |
| Abstraction | Hiding unnecessary details |
| Constructor | Initializes an object |
| Overriding | Child changes parent behavior |
## 22. Conclusion
OOP is an important part of Python programming.
It helps developers build programs using classes and objects.
The four main principles are:
1. **Encapsulation** – keeps data organized and protected.
2. **Inheritance** – allows code to be reused.
3. **Polymorphism** – allows different behaviors through the same interface.
4. **Abstraction** – hides unnecessary implementation details.
OOP makes Python programs easier to organize, reuse, maintain, and expand.
## References
1. Python Documentation – Object-Oriented Programming.
2. Python Documentation – Classes.
3. Python Documentation – Inheritance.
4. Python Documentation – Abstract Base Classes.