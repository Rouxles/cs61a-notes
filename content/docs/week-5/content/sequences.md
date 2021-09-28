---
title: "Sequences"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Sequences

## Lists in Environment Diagrams

Lists can represented with box and pointer notation (similarly to functions); however, unlike functions, each element in the array has its own box, and is index labelled.

![Basic box and pointer notation](https://i.imgur.com/KQgZJvx.png)

What this implies is that assigning a variable to another list will **not create a copy of that list**, but rather point towards the same list — this ends up being a correct assumption to make.

![Code Assumption](https://i.imgur.com/UQwPpGS.png)

Each box can either hold a value (for example a number or a string), or an object (for example, a function, another list, or a Class).

![Tougher box and pointer notation](https://i.imgur.com/TqnvKuA.png)

## List Slicing

Slicing a list creates a **new** list (as in it points to a separate list). The behaviour is very similar to the `range()` function — it starts on the first 'argument' provided, ends on the number right before the second 'argument', with step of the third 'argument'. In this case however, the separator is `:` rather than `,`. If there is no argument provided next to the `:`, it defaults to `0`.

Below are some examples:

```python
lst = [1, 2, "bananas"]
lst[0:] # [1, 2, "bananas"]
lst[:2] # [1, 2]
lst[1:] # [2, "bananas"]
lst[::2] # [1, "bananas"]
```

This behaviour also works with strings:

```python
string = "benbaron"
string[3:] # "baron"
string[:3] # "ben"
```

## Small Practice Problems

### Recursion in Lists

Imagine summing the numbers in a list but using recursion rather than iteration or the `sum()` function.

```python
def sum_numbers(lst):
    '''Returns the sum of the numbers in lst
    >>> sum_numbers([2, 3, 4])
    9
    '''
```

We could implement the function above using list comprehension:

```python
def sum_numbers(lst):
    '''Returns the sum of the numbers in lst
    >>> sum_numbers([2, 3, 4])
    9
    '''
    if lst == []: # base case
        return 0
    else:
        return lst[0] + sum_numbers(lst[1:]) 
        # takes the first number and 
        # recursively calls the function on a smaller list.
```

### Reversing a String (Recursively)

```python
def reverse_string(word):
    '''Reverse the string provided in word
    >>> reverse_string("ben")
    neb
    '''
```

Our base case here would be when the word provided is an empty string.

```python
def reverse_string(word):
    '''Reverse the string provided in word
    >>> reverse_string("ben")
    neb
    '''
    if word == "":
        return ""
    else:
        return reverse_string(word[1:]) + word[0]
        # keep in mind the order of the operation above matters
        # word[0] is put afterwards because
        # that should be added up later
```

## Built-in functions for Iterables