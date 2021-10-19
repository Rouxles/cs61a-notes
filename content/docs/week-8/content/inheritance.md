---
title: "Inheritance"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Inheritance

Inheritance is a powerful tool that is very often used to reduce redundant code. If you have more specific versions of a larger class, inheritance can be extremely useful. Using our `Animal` class from the **Objects** notes, we can use all its general attributes, but then add more specific classes.

```python
class Animal:
    default_food = []
    def __init__(self, name, energy = 100):
        self.name = name
        self.food = self.default_food[:]
        self.energy = energy
        self.times_fed = 0

    def feed(self, food):
        self.food = self.food + [food]
        self.times_fed += 1
        self.energy += 10

    def play(self):
        if energy <= 20:
            return "Not Enough Energy"
        self.energy -= 20
        self.is_happy = True # Creates new instance variable
        return f"{self.name} has {self.energy} energy."

my_cat = Animal("Sochi")
my_cat.feed("Tuna")
```

Instead of making `my_cat` an instance of the `Animal` class, we could instead create a `Cat` class that **inherits** from the `Animal` class - meaning that it contains the same class, methods, and instance variables as the `Animal` class (which can then be overridden).

The syntax for creating a class inherited from another class is shown below:

```python
class Cat(Animal):
    pass
```

Right now, this will create a new `Cat` class pointing towards the `Animal` class we've already created, meaning that it can also access the class attributes/variables alongside the methods of the `Animal` class.