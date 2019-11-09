---
description: 'Brief read on python - https://www.python.org/'
---

# Pythonism

## Overview

* Files end with `.py` 
* Uses _**indentation**_ to indicate block scope
* Dynamically typed variables and created only after value is assigned to it
* Can use `""` or `''` for string variables
* Comment with `#` 
* Has 3 type of number \(int `1` , float `1.1`, and complex `1j` \)
* Can use `type()` function to get type of variable
* Casting done using constructor function `int()` `float()` `str()` 
* Can assign multi line string using 3 single `''' '''` or double `""" """` quotes
* String are array of string
* Set of built-in string util methods [https://www.w3schools.com/python/python\_ref\_string.asp](https://www.w3schools.com/python/python_ref_string.asp)
* logical operator uses \(`and` `or` `not()` \)
*  `is` and `is not` operator can be used to check if object are same and they point to same memory location 
* `in` and `not in` operator can be used to check if a sequence exist inside another variable
* function defined using `def` 
* has lambda \(anonymous function\) feature
  * `lambda arguments : expression` 
  * \(need to use keyword `lambda`\) `x = lambda a : a + 1` 
* Uses `try` `except` `finally` for `try catch finally` 
* PIP used as package management [https://pypi.org/](https://pypi.org/)
* `format()` method used to format string. ie. to have a place holder in string  

{% tabs %}
{% tab title="format-example.py" %}
```python
name = "madan"
greet = "Hello, {}" 

#prints Hello, madan.
print(greet.format(name)   
```
{% endtab %}
{% endtabs %}

In python we can pass a special symbol on argument to represent arguments that could be in any number. These are `*args` and `**kwars` .

`*args` represents all the arguments that don't have key/value \(tuples\) pair. 

`**kwars` represents all the arguments with `key=value` \(dictionary\) pairs.

#### **Collections**

* **List** is a collection which is ordered and changeable. Allows duplicate members. \(_Like_ `array`\)
  * `["example", "of", "list"]`
  * List built-in methods : [https://docs.python.org/3/tutorial/datastructures.html](https://docs.python.org/3/tutorial/datastructures.html)
* **Tuple** is a collection which is ordered and unchangeable. Allows duplicate members. \(_Property similar to Immutable/Cons_t\)
  * `("example", "of", "tuple")`
* **Set** is a collection which is unordered and unindexed. No duplicate members.
  * `{"example", "of", "set"}`
  * Once set is created - we can't change the items but can add/remove the items
* **Dictionary** is a collection which is unordered, changeable and indexed. No duplicate members.
  * {"name": "example", "second\_name": "of", "last\_name": "dictionary"}
  * Key and Value mapping

## Object Orientation

#### Class

Uses `class` keyword to declare class, `class x:` 

Classes have a built-in function \(_constructor\)_ `__init__()` called when the object is being created. 

`self` parameter naming convention is used for reference to current instance of class \(similar to  `this` in other languages\), however it can be any name but has to be the first parameter in any method inside the class.

Classes can have their own methods.

`del` keyword can be used to deleted a object property or the object itself

```python
class Life:
    def __init__(self, name):
        self.name = name
        
    def lifeupdate(self):
        print("Hello, name is " + self.name)

# create new object using class        
newLife = Life("madan")

# assign new value to property
newLife.name = "apple"

# del property form object
del newLife.name

# del object itself
del newLife

```

#### Inheritance

To inherit a _**parent**_ class by _**child**_ class in python, we need to send the _**parent**_ class as a parameter in _**child**_ class.

`pass` is keyword used to tell python that nothing should be there.

It can be used after the function to give an empty function or after the class to act as a placeholder.  After declaring function/class, if we leave the next line/block empty, python will throw `IndentationError` 

Hence, we can use `pass` keyword when we don't want to add any other properties or methods to the class

```python
class GoodLife(Life):
    pass
```

Similar to other language, we can use the constructor function and call parent function \(like `super.parentFn()`\)

```python
class OkayLife(Life):
    def __init__(self, name):
        #calling parent constructor fn to keep the inheritance
        Life.__init__(self, name, ourdreamproperty)
        #sepecific property of okaylife class
        self.dream = ourdreamproperty
```

## Module

In python module can be considered as just any file containing a set of functions or variables which we can include in our code. 

When using the module:

* import the module `import mymodule`
* use `modulename.modulefunctionname` syntax to use the function
* we can also use alias to a module by using `as` keyword `import mymodule as universe` 
* we can also import parts of module using `from` keyword `from mymodule import earth` , also we won't have to prefix with module name whilst using `from` keyword to import only a specific part of module
* 
{% tabs %}
{% tab title="mymodule.py" %}
```python
def firework(sound):
    print("Firework sound: " + sound)
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="myapp.py" %}
```python
import mymodule

mymodule.firework("Quack quack")
```
{% endtab %}
{% endtabs %}

