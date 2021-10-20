---
title: "Representation"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# String Interpolation

This is not part of representation, but is instead an **extremely** useful tool to make writing strings with multiple variables far cleaner. You may have already seen me use string interpolation earlier on in the course.

In Python, the cleanest way to use string interpolation is with an `f-string`, where the letter `f` is appended before quotation marks.

```python
f""
```

You can see the syntax highlighting sees the `f` in a different colour! With this notation, we can then put expressions in our string itself and have them evaluate to 'proper' values. Different languages deal with string interpolation in different manners.

```python
one = 1
two = "two"
five = "five"
f"{one + 1} {two}, {five}" # will return "2 two, five"
```

# Representation

## Built-in Object Attributes

In Python, every built in type **inherits** from `object`. Everything in Python is an object of some sort. As a result, they all have their own `dunder` methods that are different for every object.

If you run `dir()` on an object (which could be a string, list, or something else), you will see a list of its methods. Behind the scenes, Python runs these `dunder` methods, so we don't really need to worry about those (kind of like data abstraction if you think about it)

## String Representation

The `__str__` method returns a string representation made to be **human readable**.

For example, let's define our own class for `Rational` numbers (similarly to the data abstraction we were using earlier)