
### 1. What is `on_delete=models.CASCADE`?
 `CASCADE` deletes the related child records when the parent record is deleted.  
> For example, deleting a `Question` will also delete its related `Choice` records.

### 2. What are Django Model Fields?
- Model fields define the type of data stored in a database, such as `CharField`, `IntegerField`, `DateTimeField`, and `BooleanField`.  
- They also define properties like maximum length, default value, nullability, and uniqueness.

### 3. What are Django Validators?
 Validators are functions used to check whether a value is valid before it is saved or accepted.  
> Examples include `MinValueValidator`, `MaxValueValidator`, `MinLengthValidator`, and `RegexValidator`.

### 4. What is the difference between a Python Module and a Python Class?
- A **module** is a Python file containing code such as functions, classes, and variables.  
- A **class** is a blueprint used to create objects containing data and methods.