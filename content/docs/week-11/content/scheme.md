---
title: "Scheme"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Scheme

Scheme is another programming language that CS61A can test. The reason why this is taught is not only because you make an interpreter for Scheme as your final CS61A project (where you write code in Python to essentially execute scheme code in Python - it's really cool), but also because it's essentially a practical way of showing that you're able to quickly pick up other languages after you get comfortable with one.

Scheme isn't really used that often in actual codebases, but it's a pretty good method of teaching **functional programming** due to the restrictions it has in comparison to Python. (For example, Scheme doesn't allow you to do any sort of iteration, and also lists can only be of the Linked list form, meaning that many of the programming problems are solved using recursion)

## Scheme Expressions

Nearly everything in Scheme is executed the same - basically everything boils down to **call expressions**, even basic operations like `+` and `/`.

```scheme
(+ 1 2) ; 3
(/ 4 2) ; 2
(quotient 5 2) ; 2
(modulo 5 2) ; 1
```

A Python equivalent for the first line would be the following:

```python
from operator import add
add(1, 2) # which is the same as 1 + 2
```

Notice how there's consistent syntax? When you want to call something, you just wrap it in a set of parentheses, then you supply your operators and operands in the same order as call expressions in Python. The execution order of this call expression matches that of Python - it first looks at the operator and sees whether it can be a function, then evaluates the operands from left to right and after that is done, passes it into the operator.

```scheme
(/ (+ 2 2) 2) ; 2
```

You can also nest expressions in expressions.

## Special Forms

Everything in Scheme that doesn't behave the same way as a call expression is a **special form**.

- `if` expression
  - `(if <condition> <true-block> [<false-block>])`
  - This will check whether `<condition>` is truthy (more on this later, it behaves differently to Python), then will execute `<true-block>` if it is, else will execute `<false-block>` if it's provided.
- `and`/`or`
  - `(and <e1> <e2> ... <en>)`
  - `(or <e1> <e2> ... <en>)`
  - Behaves pretty much the same as Python `and`/`or` other than the truthy values.
- `define` - assignment in scheme
  - `(define <symbol> <expression>)`
    - Assignment in Scheme (assigning an expression to a symbol)
  - `(define (<symbol> <parameters>) <body>)`
    - Assignment in Scheme but for functions instead (this is shorthand for making a lambda function then assigning that to a symbol - more on this later)

### Define Form

```scheme
(define x 2) ; x
x ; 2
```

The code above will evaluate the expression `2`, then binds that value to the name `x`. This name has to be a valid scheme symbol (so it can't be integers for instance).

#### Define Prodedure

```scheme
(define (square x) (* x x))
```

The code above will make a `lambda` function that takes in a parameter `x` and when called, will multiply `x` by itself. This code is equivalent to the following:

```scheme
(define square (lambda (x) (* x x)))
```

### If Expression

In Scheme, everything that isn't `#f` (which is the Scheme equivalent of `False`) is a *truthy* value. **This is different to Python's behaviour - remember to keep this in mind when you're writing in scheme**

Example: Code that returns the length of non-empty lists, else returns 0 for empty lists.

```scheme
(define lst (list 1 2 3))

(if (null? lst) 0 (length lst)) ; null? and length are built-in procedures
```

You can find all these built in procedures on CS61A's official website.

### Cond Expression

This special form allows for `if ... elif ... else` statements because the normal `if` expression that Scheme uses does not allow for multiple conditions. However, this `cond` expression allows for something similar to this to occur.

```scheme
(define x 2)

(cond
    ((> x 2) 'hi)
    ((> x 50) 'ben)
    (else 'not hi)
) ; not hi
```

### Lambda Expressions

`lambda` expressions evaluate to anonymous procedures (when not in a `define` expression). They are written `(lambda ([param] ...) <body>)`. These lambdas can also be call expressions.

```scheme
(lambda (x) (* x 2))
((lambda (x) (* x 2)) 4) ; 8
```

### `let`

`let` in Scheme is pretty similar to `define` other than the scope that the variable is in. In essence, `define` when used will make a variable accessible in the global frame, but `let` will only make a variable that's accessible in the function's frame (Python's default behvaiour).

## Scheme Lists

All lists in Scheme are linked lists, similar to the `Link` class we were using earlier on in Python.

```python
Link(1, Link(2))
```

The Scheme equivalent to the linked list we made above is 

```scheme
(cons 1 (cons 2 nil))
```

where `nil` is our `Link.empty`. This `nil` is required in Scheme when we use the `cons` expression.

You can also define lists in the following manner:

```scheme
(define lst_one (list 1 2 3))
lst_one ; (1 2 3)
(define lst_two (list 1 (list 2 3) 4))
lst_two ; (1 (2 3) 4)
(define lst_three '(1 2 3))
lst_three ; (1 2 3)
(define lst_four '(1 (list 2 3) 4))
lst_four ; (1 (list 2 3) 4) - notice how this one doesn't evaluate anything
```

### Accessing elements in our List

In Python:

```python
ll = Link(1, Link(2))
ll.first # 1
ll.rest # Link(2)
```

Scheme Equivalent:

```scheme
(define lst (list 1 2 3))

(car lst) ; 1
(cdr lst) ; (2 3)
```

Names are weird - but you have to remember them. There is a historical reason for these chosen names, but I won't cover them here because I don't think it's particularly too important to know at the moment. If you're interested, take a look at [this link](https://en.wikipedia.org/wiki/CAR_and_CDR).

## Symbolic Programming

Usually, symbols refer to values:

```scheme
(define a 1)
(define b 2)
(list a b) ; (1 2)
```

However, we can use quotation to refer to the symbols directly:

```scheme
(define a 1)
(define b 2)
(list 'a b) ; (a 2)
```

This is shorthand for the `quote` form:

```scheme
(list (quote a) b) ; (a 2)
```
