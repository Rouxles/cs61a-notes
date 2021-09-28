---
title: "Data Abstraction + Dictionaries"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Data Abstraction

Many values in programs are compound values — a value composed of multiple values (for example coordinates, dates, or geographic positions)

By using a **data abstraction**, you can manipulate compound values as units **without needing to worry about the way that values are stored**.

## Pair Abstraction

For data that is stored in pairs, we can manipulate these values using a `pair` data abstraction:

```python
couple = pair("a", "b")
a = first(couple)
b = second(couple)
```

By implementing `pair()` (our constructor), `first()`, and `second()` (the selectors), you can access these elements without needing to worry about how the data is stored. The only time that people need to worry about how the data is stored is when implementing the functions themselves. **One** example (implying that there are multiple ways) of implementing these functions can be seen below:

```python
couple = lambda a, b: [a, b]
first = lambda lst: lst[0]
second = lambda lst: lst[1] 
```

### Rational Numbers

One reasonable data abstraction to do is to implement rational numbers as a data abstraction. By storing the numerator and denominator separately, we can get precise values of certain fractions such as `1/3`.

For example:

```python
half = rational(1, 2)
top = numerator(half) # 1
bottom = denominator(half) # 2
```

We have the structure for a denominator... cool I guess? But at its current state, we can't do anything with the numbers in terms of multiplying/adding/printing them in the way that we expect. As a result, we can write more functions to help us do that using functions.

```python
def mul_rational(x, y):
    return rational(
        numerator(x) * numerator(y),
        denominator(x) * denominator(y)
    )

def add_rational(x, y):
    nx, dx = numerator(x), denominator(x)
    ny, dy = numerator(y), denominator(y)
    return rational(
        nx * dy + ny * dx, 
        dx * dy
    )
```

Notice how at this point we **still do not know how `rational()` is implemented**.

## Layers of Abstraction

why use data abstraction?

(also makes programs to change easier cause implementations changing is easier)

# Dictionaries

mapping of `key-value` pairs