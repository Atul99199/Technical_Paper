# SOLID Principles in Python

## Introduction

**SOLID** is a collection of 5 principles used to write clean, maintainable, and flexible code.

SOLID stands for:

* **S** — Single Responsibility Principle
* **O** — Open/Closed Principle
* **L** — Liskov Substitution Principle
* **I** — Interface Segregation Principle
* **D** — Dependency Inversion Principle

Let's understand each principle with a **small and simple example**.

---

# 1. S — Single Responsibility Principle (SRP)

## Meaning

> A class should have only **one job**.

Imagine a person who does three jobs:

* Cooking
* Driving
* Teaching

It is better to separate these responsibilities.

###  Bad Example

```python
class Student:
    def study(self):
        print("Student is studying")

    def save_to_database(self):
        print("Saving student to database")

    def print_report(self):
        print("Printing report")
```

The `Student` class is doing too many things:

* Student behavior
* Database work
* Report generation

###  Better Example

Separate the responsibilities.

```python
class Student:
    def study(self):
        print("Student is studying")


class StudentDatabase:
    def save(self):
        print("Saving student to database")


class StudentReport:
    def print_report(self):
        print("Printing report")
```

Now each class has **one responsibility**.

### Easy way to remember

**S = Single Job**

> One class → One main job.

---

# 2. O — Open/Closed Principle (OCP)

## Meaning

> A class should be **open for extension** but **closed for modification**.

In simple words:

**We should be able to add new functionality without changing existing code.**

###  Bad Example

```python
class Payment:
    def pay(self, method):
        if method == "cash":
            print("Paid by cash")
        elif method == "card":
            print("Paid by card")
```

If we want to add UPI, we need to modify the `Payment` class.

```python
elif method == "upi":
    print("Paid by UPI")
```

This can become difficult when there are many payment methods.

###  Better Example

Create separate classes.

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

Now we can add another payment method without changing the existing classes.

```python
class PayPalPayment:
    def pay(self):
        print("Paid by PayPal")
```

### Easy way to remember

**O = Open to add, Closed to change**

> Add new features without changing old working code.

---

# 3. L — Liskov Substitution Principle (LSP)

## Meaning

> A child class should be usable wherever its parent class is expected.

This sounds difficult, but the idea is simple.

If we say:

> A dog is an animal.

Then a `Dog` should behave like an `Animal`.

### Example

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    def speak(self):
        print("Dog says Woof")
```

We can use `Dog` wherever an `Animal` is expected.

```python
def make_sound(animal):
    animal.speak()


dog = Dog()

make_sound(dog)
```

### Output

```text
Dog says Woof
```

This works because `Dog` follows the behavior expected from `Animal`.

### Simple Bad Example

Imagine this:

```python
class Bird:
    def fly(self):
        print("Bird is flying")


class Penguin(Bird):
    def fly(self):
        raise Exception("Penguins cannot fly")
```

Now:

```python
def make_bird_fly(bird):
    bird.fly()


penguin = Penguin()
make_bird_fly(penguin)
```

The program fails.

The problem is that `Penguin` should not be forced into a design where every `Bird` must fly.

### Better Design

```python
class Bird:
    def eat(self):
        print("Bird is eating")


class FlyingBird(Bird):
    def fly(self):
        print("Bird is flying")


class Penguin(Bird):
    pass


class Eagle(FlyingBird):
    pass
```

Now only birds that can fly inherit from `FlyingBird`.

### Easy way to remember

**L = Child should work like the parent**

> A child class should not break the expectations of the parent class.

---

# 4. I — Interface Segregation Principle (ISP)

## Meaning

> A class should not be forced to use methods that it doesn't need.

Python does not require traditional interfaces like some other languages, but we can still understand the principle using classes.

###  Bad Example

Suppose we create a large `Machine` class.

```python
class Machine:
    def print_document(self):
        pass

    def scan_document(self):
        pass

    def fax_document(self):
        pass
```

Now imagine a simple printer.

```python
class SimplePrinter(Machine):

    def print_document(self):
        print("Printing document")

    def scan_document(self):
        raise NotImplementedError

    def fax_document(self):
        raise NotImplementedError
```

The printer does not support scanning or faxing, but it is forced to implement those methods.

###  Better Example

Separate the responsibilities.

```python
class Printer:
    def print_document(self):
        print("Printing document")


class Scanner:
    def scan_document(self):
        print("Scanning document")


class Fax:
    def fax_document(self):
        print("Faxing document")
```

A simple printer only needs:

```python
printer = Printer()

printer.print_document()
```

A multifunction machine can use all three:

```python
class MultiFunctionMachine(Printer, Scanner, Fax):
    pass
```

### Easy way to remember

**I = Interface should be small**

> Don't force a class to implement things it doesn't need.

---

# 5. D — Dependency Inversion Principle (DIP)

## Meaning

> A class should depend on an **abstraction**, not directly on a specific class.

This sounds complicated, so let's use a simple example.

Imagine an `Order` class that directly creates an email service.

###  Bad Example

```python
class Email:
    def send(self):
        print("Sending email")


class Order:
    def __init__(self):
        self.email = Email()

    def place_order(self):
        print("Order placed")
        self.email.send()
```

The `Order` class is directly connected to `Email`.

If we want SMS instead, we have to change the `Order` class.

---

##  Better Example

Let the `Order` class receive the notification service from outside.

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
```

Now we can use email:

```python
email = Email()

order = Order(email)
order.place_order()
```

Output:

```text
Order placed
Sending email
```

Or we can use SMS:

```python
sms = SMS()

order = Order(sms)
order.place_order()
```

Output:

```text
Order placed
Sending SMS
```

We didn't have to change the `Order` class.

This technique is called **Dependency Injection**.

### Easy way to remember

**D = Depend on abstraction, not a specific thing**

> Give a class what it needs instead of making it create everything itself.

---


# 6. SOLID Quick Revision

| Letter | Principle             | Simple Meaning                               |
| ------ | --------------------- | -------------------------------------------- |
| **S**  | Single Responsibility | One class → One job                          |
| **O**  | Open/Closed           | Add new code without changing old code       |
| **L**  | Liskov Substitution   | Child should work like the parent            |
| **I**  | Interface Segregation | Don't force unnecessary methods              |
| **D**  | Dependency Inversion  | Depend on abstractions, not specific classes |

---

# 7. Easy Trick to Remember SOLID

Think of SOLID like this:

 - **S** — One job
 - **O** — Add without changing
 - **L** — Child should fit parent
 - **I** — Keep interfaces small
 - **D** — Don't depend directly on concrete classes

 # 8. Referance 

1. Python Software Foundation. "Abstract Base Classes — `abc`." Python Documentation.
   https://docs.python.org/3/library/abc.html

2. Python Software Foundation. "Protocols and Structural Subtyping." Python Typing Documentation.
   https://typing.python.org/en/latest/spec/protocol.html

3. Python Software Foundation. "Classes." Python Documentation.
   https://docs.python.org/3/tutorial/classes.html

4. YouTube Tutorial  : https://www.youtube.com/playlist?list=PL6n9fhu94yhXjG1w2blMXUzyDrZ_eyOme




