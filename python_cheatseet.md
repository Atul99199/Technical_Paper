# python_cheetsheet

<table>
<tr>
<th>1. List / Array Methods</th>
<th>2. String Methods</th>
</tr>

<tr>
<td valign="top">

Python uses **lists** as dynamic arrays. Lists can store multiple values and can be changed after creation.

- `append(x)` → Adds one item at the end
- `extend(x)` → Adds multiple items
- `insert(i, x)` → Adds item at index `i`
- `remove(x)` → Removes first matching value
- `pop(i)` → Removes and returns item
- `sort()` → Sorts the list
- `reverse()` → Reverses the list
- `index(x)` → Returns item's index
- `count(x)` → Counts occurrences
- `clear()` → Removes all items
- `len(list)` → Returns number of items

</td>

<td valign="top">

Strings are sequences of characters. Python strings are **immutable**, meaning their original value cannot be changed.

- `upper()` → Converts to uppercase
- `lower()` → Converts to lowercase
- `title()` → Capitalizes each word
- `strip()` → Removes spaces from ends
- `replace(a,b)` → Replaces text
- `split()` → Converts string to list
- `join()` → Combines list into string
- `find(x)` → Returns position of text
- `count(x)` → Counts occurrences
- `startswith(x)` → Checks beginning
- `endswith(x)` → Checks ending
- `isalpha()` → Checks alphabets
- `isdigit()` → Checks digits

</td>
</tr>


<tr>
<th>3. Objects & Object-Oriented Programming</th>
<th>4. Decorators</th>
</tr>

<tr>
<td valign="top">

OOP organizes code using **classes and objects**.

- **Class** → Blueprint for objects
- **Object** → Instance of a class
- **Encapsulation** → Combines data and methods
- **Inheritance** → Reuses parent class code
- **Polymorphism** → Same method, different behavior
- **Abstraction** → Hides unnecessary details

**Example:**

<pre><code>class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)

student = Student("Atul")
student.show()</code></pre>

</td>

<td valign="top">

A decorator is a function that **adds or changes the behavior of another function without modifying its original code**.

Common uses: logging, authentication, validation, timing and caching.

**Example:**

<pre><code>def decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@decorator
def greet():
    print("Hello")

greet()</code></pre>

`@decorator` is shorthand for applying the decorator to a function.

</td>
</tr>


<tr>
<th>5. virtualenv</th>
<th>6. pip Package Manager</th>
</tr>

<tr>
<td valign="top">

A virtual environment creates an **isolated Python environment** for a project. It prevents dependency and version conflicts between projects.

**macOS / Linux:**

<pre><code>python -m venv venv
source venv/bin/activate
deactivate</code></pre>

**Windows:**

<pre><code>python -m venv venv
venv\Scripts\activate
deactivate</code></pre>

Each project can have its own package versions.

</td>

<td valign="top">

`pip` is Python's package manager. It is used to install, remove and manage external libraries.

**Common commands:**

<pre><code>pip install requests
pip uninstall requests
pip list
pip show requests
pip freeze
pip install -r requirements.txt
pip freeze > requirements.txt
pip install --upgrade requests</code></pre>

`requirements.txt` stores project dependencies so they can be installed again easily.

</td>
</tr>


<tr>
<th>7. PEP 8 Standards</th>
<th>8. Quick Revision</th>
</tr>

<tr>
<td valign="top">

PEP 8 is the official **Python style guide**. It helps developers write consistent and readable code.

- Use **4 spaces** for indentation.
- Functions/variables → `snake_case`
- Classes → `PascalCase`
- Constants → `UPPER_CASE`
- Use spaces around operators.
- Keep imports at the top.
- Use meaningful names.
- Separate functions/classes with blank lines.
- Keep lines generally within **79 characters**.

</td>

<td valign="top">

- **List** → Mutable collection of items
- **String** → Immutable sequence of characters
- **Class** → Blueprint for objects
- **Object** → Instance of a class
- **Decorator** → Extends function behavior
- **virtualenv** → Isolated Python environment
- **pip** → Package manager
- **PEP 8** → Python coding style guide

</td>
</tr>

</table>
