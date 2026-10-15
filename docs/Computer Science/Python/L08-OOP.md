
# Object-Oriented Programming (OOP) 
> Course source: CS50P Lecture 08

Object-Oriented Programming is a programming paradigm where you transition from writing code step-by-step (procedurally) to **creating custom blueprints and data types** (classes) .



## Core OOP Terminology
OOP is based on the concept of objects, defined by and associated with two things:

* Attributes: data
* Methods: functions

The most important feature: **methods** associated with the objects can **access and modify the attributes** of the objects via **`self.` keyword**.

| Concept | Purpose | Syntax| Details  | Behavior / Effect |
| :--- | :--- | :--- | :--- | :--- |
| **[Class](https://docs.python.org/3/tutorial/classes.html)** | Acts as a custom blueprint or template to invent our own data type for modelling **a real world entity** and give it a name. | `class ClassName:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`...` | **Class name** should be **Capitalized** by convention. The `...` is a placeholder indicating the code will be finished later. | Defines the attributes and behaviors that objects of this type will have. |
| **Objects / Instances** | Individual, concrete creation built using a class blueprint. An object is an instance of the class.| `instance = ClassName()` | Created using the class constructor syntax. | Inherits all structure and methods defined in the class. |
| **Attributes (instance variables)**| Variables stored inside an object or class and operate on **each instance**. | Within def: <br>`self.attribute = value` <br> <br> Outside def:<br>`instance.attribute = value` | **Accessed and set** using **dot notation**. | Standardizes the data that belongs to an instance. We can make it **inmutable or mutable**. |
| **Instance Methods** | Functions defined inside a class that dictates how **each instance** behave. |  Within def: <br> `self.method()`<br><br> Outside def:<br>`instance.method()` | Must take **`self`** as its first parameter to refer to the current object. | Allows objects to perform **custom actions** and **manipulate their own data**. |
| **Class variables**| **Shared variables** for the **entire class** or across **all the instances of the class**, exist within class itself. | Within def: <br> `class ClassName:`<br>&nbsp;&nbsp;&nbsp;&nbsp;`class_variable = value` | |

### Class Definition Template
encapsulate all the functionality of a class within the class definition. 
```python
class ClassName(object_type):
     class_variable = value

     def __init__(self,argument_1, argument_2 = default_value,...): 
          self.attribute_1 = argument_1   # Note: no leading underscore (`_attribute`) in __init__ to make sure even this assignment goes through the setter. Without _, we are calling the getter and setter methods, not the actual attribute.  
          self.attribute_2 = argument_2   

     def __str__(self): 
          return f"{self.attribute}"
     
     def __add__(self, other):
          attribute_1 = self.attribute_1 + other.attribute_1
          attribute_2 = self.attribute_2 + other.attribute_2
          return ClassName(attribute_1, attribute_2)

     # getter and setter (similar for all the attributes)
     #  The `@property` (getter) must be defined before the `@<property>.setter`. 
     @property
     def attribute_1(self):
          return self._attribute_1
     
     @attribute_1.setter
     def attribute_1(self, argument):
          if argument not in [...]:    # validate attributes before assignments (and catch errors using try-except block when creating instances)
               raise SpecificErrorType("ErrorMessage")
          self._attribute_=1 = attribute_1

    @classmethod
    def get(cls, arguments):
        variable_1 = input("string prompt: ")
        variable_2 = input("string prompt: ")
        # create an new instance of the class
        return cls(variable_1, variable_2) 

def main():
    instance_name = ClassName.get()

if __name__ == "__main__":
    main()
```


### Special Magic Methods [\_\_name\_\_](https://rszalski.github.io/magicmethods/)
If we define these [Python special methods](https://docs.python.org/3/reference/datamodel.html#special-method-names), Python would automatically call them.

| Special Method | Purpose | Syntax | Parameters | Return Value  |
| :--- | :--- | :--- | :--- | :--- |
| **`__init__`** | The initialization method standardizes and **initializes object attributes** upon creation <br><br> (The construct method is `__new__` but we do not need to deal with it). | `def __init__(self, argument):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`self.attribute = argument` | - **`self`**: Refers to the **current object** being created. <br>- **Custom arguments** passed during instantiation. | Returns `None` automatically. Triggered by calling the class itself (e.g., **constructor** `ClassName(args)`). |
| **`__str__`** | Defines how the object should represent itself as a text string for **users**. The return string is displayed automatically when the **object is printed** (e.g., **`print(instance)`)**| `def __str__(self):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`return f"{self.attribute}"` | - **`self`**: The current object. | **Must return a string**. |
| **`__repr__`** |	Provides the “official” string **representation** that shows more info (type) (used in the Python shell, debugging, etc.) for developers|
| **`__add__`** | **Operator Overloading**: **Customizes** how the `+` operator behaves between two objects. | `def __add__(self, other):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`return ...` | - **`self`**: The object on the left of `+`.<br>- **`other`**: The object on the right of `+`. | Returns a new object (or custom value) representing the sum of both objects. |

### Getter and Setter - Define Properties using Decorators 
To validate or restrict attributes before it is assigned to any values and avoid wrongly assignment, we define properties using function decorators (which begin with **`@`**)
 

| Decorator | Purpose | Syntax | Associated Parameter | Note |
| :--- | :--- | :--- | :--- | :--- |
| **`@property`** | Defines a **getter** function to **safely** read an attribute. <br><br> Note: The `@property` (getter) **must** be defined before the `@<property>.setter`. | `@property`<br>`def attribute(self):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`return self._attribute` | **`self`** | `@property` only and **omitting the `@<property>.setter`** decorator creates a **read-only** property. <br> It will be called **automatically** whenver we **access the attribute via `.attribute`** <br><br>Note the **leading underscore (`_attribute`)**, which flags to programmers that this variable **should not be modified directly**. Python does not have the **private/public** keywords like C++, make sure **not** to touch the attributes with any **leading underscore (`_attribute`)** outside the class.|
| **`@<attribute>.setter`** | Defines a **setter** function to validate data before it is saved.   | `@attribute.setter`<br>`def attribute(self, argument):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`if attribute not in [...]:`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`raise ValueError()`<br>&nbsp;&nbsp;&nbsp;&nbsp;`self._attribute = argument` | - **`self`** <br>- **`argument`**: The new value being assigned. | It will be called **automatically** whenver we **access the attribute via `.attribute = new_value`** |
| **`@classmethod`** | The function defined inside the class to add functionality to the **class itself as a whole**, not to each individual instance of that class. It does **not** have access to the object itself **`self`** but the class itself **`cls`** | `@classmethod`<br>`def class_method_name(cls, arguments):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`return cls(variables) # create an object of current class` | **`cls`**: Refers to the **class** itself, **replacing** the standard instance **`self`**. | Can be **called directly on the capitalized class name** (e.g., `ClassName.class_method_name()`) **without** instantiating an object first. |
|**`@staticmethod`** |

### Built-In Type Checking (`isinstance`)

| Method | Purpose | Syntax | Parameters  | Return Value|
| :--- | :--- | :--- | :--- | :--- |
| **`isinstance()`** | Checks whether an object is an instance of a specified class or data type (or tuple of types). | `if not isinstance(object, classinfo):`<br>&nbsp;&nbsp;&nbsp;&nbsp;`raise ValueError("")` | - **`object`**: The variable/instance to inspect.<br>- **`classinfo`**: A type (e.g., `int`, `str`, any class) or tuple of types (e.g., `(int, float)`). | Returns **`True`** if the object matches the specified class/type; returns **`False`** otherwise. |


## Advanced Features
### Inheritance
Allows a "child" class to **inherit** all the variables, attributes, and methods from its **"parent" or ""gradparent"** class. Eliminates redundant code when multiple classes share the same parameters and codes. We can even overwrite it if we want the child class to behave a bit differently than its parent class.

```python
class Parent:
     def __init__(self, argument_1):
        if not argument_1:
            raise ValueError("Missing argument_1")
        self.argument_1 = argument_1

class Child(Parent):
     def __init__(self, argument_1, argument_2):
          super().__init__(argument_1)
          self.argument_2 = argument_2
```

| Concept | Purpose | Syntax Example | Explanatory Details |
| :--- | :--- | :--- | :--- |
| **`super()`** | **Access the parent (or "super") class** of the current class, letting the child call the parent methods. | `super().__init__(shared_arguments)` | Used inside a child's `__init__` constructor to reuse the parent's initialization logic. |

#### Connecting to Exceptions Hierarchy
Python’s own exception system relies entirely on OOP inheritance. All exceptions are classes structured in a hierarchical parent-child tree:
```text
BaseException
 +-- KeyboardInterrupt
 +-- Exception
      +-- ArithmeticError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- KeyError
      +-- NameError
      +-- SyntaxError
      |    +-- IndentationError
      +-- ValueError
 ...
```
This is why catching a parent exception like `Exception` also catches child exceptions like `ValueError`.

