# Technical Paper: SOLID Principles in Python

## 1. Introduction
SOLID is a set of five principles for writing clean, flexible, and maintainable code.
They help organize code, reduce dependencies, and make changes easier.
- **S** — Single Responsibility
- **O** — Open/Closed
- **L** — Liskov Substitution
- **I** — Interface Segregation
- **D** — Dependency Inversion

## 2. Single Responsibility Principle (SRP)

A class should have one main responsibility or job.
A class should not handle unrelated tasks such as database work and report generation.

### Example

```python
class Student:
    def study(self):
        print("Student is studying")

class StudentDatabase:
    def save(self):
        print("Saving student")

class StudentReport:
    def print_report(self):
        print("Printing report")
```

Each class now has one clear job.

**Remember:** S = Single Job.

## 3. Open/Closed Principle (OCP)

A class should be open for extension but closed for modification.
New features should be added without changing existing working code.

### Example

```python
class CashPayment:
    def pay(self):
        print("Paid by cash")

class CardPayment:
    def pay(self):
        print("Paid by card")

class UPIPayment:
    def pay(self):
        print("Paid by UPI")
```

A new payment method can be added without changing old classes.

**Remember:** O = Open to add, Closed to change.

## 4. Liskov Substitution Principle (LSP)

A child class should work wherever its parent class is expected.
It should not break the behavior expected from the parent.

### Example

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Dog says Woof")

def make_sound(animal):
    animal.speak()

make_sound(Dog())
```

`Dog` can safely be used as an `Animal`.

### Bad Example

```python
class Bird:
    def fly(self):
        print("Flying")

class Penguin(Bird):
    def fly(self):
        raise Exception("Cannot fly")
```

A penguin should not inherit a behavior it cannot support.

**Remember:** L = Child should work like the parent.

## 5. Interface Segregation Principle (ISP)

A class should not be forced to use methods it does not need.
Keep classes and interfaces small and focused.

### Example

```python
class Printer:
    def print_document(self):
        print("Printing")

class Scanner:
    def scan_document(self):
        print("Scanning")

class Fax:
    def fax_document(self):
        print("Faxing")

class MultiFunctionMachine(Printer, Scanner, Fax):
    pass
```

A simple printer only needs printing, while a multifunction machine can use all three.

**Remember:** I = Keep interfaces small.

## 6. Dependency Inversion Principle (DIP)

A class should not depend directly on one specific service.
Instead, give it the service it needs from outside.

### Example

```python
class Email:
    def send(self):
        print("Sending email")

class SMS:
    def send(self):
        print("Sending SMS")

class Order:
    def __init__(self, notification):
        self.notification = notification

    def place_order(self):
        print("Order placed")
        self.notification.send()

Order(Email()).place_order()
Order(SMS()).place_order()
```
The `Order` class works with both Email and SMS without changing its code.
This approach is called **Dependency Injection**.

**Remember:** D = Depend on abstractions, not specific classes.

## 7. SOLID Quick Revision

| Letter | Principle | Simple Meaning |
|---|---|---|
| **S** | Single Responsibility | One class → One job |
| **O** | Open/Closed | Add features without changing old code |
| **L** | Liskov Substitution | Child should work like the parent |
| **I** | Interface Segregation | Do not force unnecessary methods |
| **D** | Dependency Inversion | Depend on abstractions |

## 8. Benefits of SOLID

SOLID principles make code:

- Easier to understand
- Easier to test
- Easier to maintain
- Easier to extend
- More reusable
- Less tightly connected

## 9. Conclusion

SOLID provides simple rules for writing better software.
The main goal is to keep classes focused and reduce unnecessary dependencies.
Using SOLID can make Python programs cleaner, flexible, reusable,
and easier to maintain.

## References

1. Python Software Foundation – Abstract Base Classes  
   https://docs.python.org/3/library/abc.html
2. Python Software Foundation – Classes  
   https://docs.python.org/3/tutorial/classes.html
3. Python Typing Documentation – Protocols  
   https://typing.python.org/en/latest/spec/protocol.html
4. YouTube Tutorial Playlist  
   https://www.youtube.com/playlist?list=PL6n9fhu94yhXjG1w2blMXUzyDrZ_eyOme