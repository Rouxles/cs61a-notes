---
title: "Control"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Control

---

## Side Effects

**Side effects** occur in functions when the function alters the global environment in some form. This could be in the form of altering a variable in the *global scope*, or using a `print` statement inside a function. One easy way to tell if a function contains side effects is that if a function acts like a mathematical function, it has no side effects.

A Mathematical function `f(x)` takes inputs and always provides the same outputs, without doing anything else. As a result, one input will never have two or more different outputs. If a programming function has the same property where certain outputs always provide the same inputs without doing anything else, it has *no side effects*

Here are a few examples:

### Example With No Side Effects

```python
def no_side_effects(x): # Squares x
    return x*x

no_side_effects(2) # >>> 4
no_side_effects(2) # >>> 4
```

In this example, every input will always map to the same output as the function does not do anything other than provide an output given an input

### Example With Side Effects

```python
ben = 1

def with_side_effects(x):
    global ben # Python usually doesn't like changing global variables so this statement is needed here
    ben += 1 # Does the same thing as ben = ben + 1
    return x*ben

with_side_effects(2) # >>> 4
with_side_effects(2) # >>> 6
```

While this example is not going to be used in a practical setting, it serves as a good example of what a side effect is. As you can see, even though we called the function `with_side_effects` twice with the same input, the output was different, which goes against the definition of a mathematical function. As a result, there is a side effect in that function.

> A side note:
> 
> While the `print` function does not change the value of any variables, it does cause a side effect by outputting something to the console, which does go against how a mathematical function works. However, while side effects are usually better to avoid where possible, `print` could sometimes be useful for debugging.
> 
> An example of a side effect that can't be avoided is writing to a file - this is necessary at times.

A function without side effects is also known as a **pure function**, while a function with side effects is also known as an **impure function**.

## The 'None' Value

In Python, any function that does not `return` a value **will return** `None`, which when printed will render `None` to the console, and when called, will not render anything in the console.

For example:

```python
def no_return(x):
    x = 1

print(no_return(2))
# >>> None
```

Note that the `print()` function has no return value, and thus will return `None` when called.

## Nested Print Statements

A nested print function is somewhat weird, but worth it to learn. 

Take this for example, what do you think will get outputted to the console? Try to think for yourself before opening the answer box below.

```python
print(print(1))
```

{{< details title="Answer" open=false >}}
```python
# >>> 1
# >>> None
```

This occurs because `print(1)` is executed first (due to the order of operations with call functions), which outputs something to console but returns `None`, so this statement is essentially equal to

```python
print(1)
print(None)
```

{{< /details >}}

For a harder example, try this one:

```python
print(print("x"), print("y"))
```

{{< details title="Answer" open=false >}}
```python
# >>> x
# >>> y
# >>> None None
```

This occurs because the call function executes the operands from left to right, so `print("x")` is called, then `print(y)`, and because both these values return `None`, the outside print function will print `None, None`.

It executes the same as the sequence below:

```python
print("x")
print("y")
print(None, None)
```

{{< /details >}}

---

## Default Arguments

---

## Boolean

A Boolean is a value that is either `True` or `False`

---

## Compound Statement

---

## While Loop

### Using a Counter Variable

---

