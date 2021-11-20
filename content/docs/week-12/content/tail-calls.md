---
title: "Tail Calls"
weight: 2
draft: true
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Tail Calls

## Recursion Efficiency

Let's take a look at a recursive and iterative implementation of a factorial function and see what the efficiency of it is.

```python
# Recursive
def recursive_factorial(n):
    if n == 1 or n == 0:
        return 1
    else:
        return n * factorial(n - 1)

# Iterative
def iterative_factorial(n):
    total = n
    while n > 0:
        n -= 1
        total *= n
    return total
```

Both of these solutions take up O(n) time, but the iterative solution reuses the variables we have, while the recursive solution needs to keep opening up frames - in fact it opens up frames an O(n) number of times, causing this to have some space efficiency issues.

This is because each recursive call opens up a new frame, and because the return expression `n * factorial(n - 1)` requires us to eventually get the factorial result, the frames we open have to stay **active**. However, in scheme, if we have a **tail-recursive** function, we only actually need a constant number of frames.

## Tail Recursion

But what exactly is a tail-recursive function?

These are essentially recursive functions where the final call doesn't require any more expression. I'll give a more concrete example later, but for now, I'll just put down a few rules about tail recursive calls (these are useful for Scheme project! You literally just need to implement the things below + Trampolining which is going to be found in the bottom of this document).

- In a tail recursive function, every recursive call must be a **tail call** (meaning that it's the last call of the whole function)
- A **tail call** is a call expression in a **tail context** if (for Scheme):
  - It's the last body sub-expression in a lambda function
  - It's sub-expressions 2 or 3 in an `if` statement
  - All the non predicate sub-expressions in `cond`
  - The last sub-expression in `let`, `begin`, `and`, and `or`

Implement all these, and you have a tail recursive function.

Let's try to make our `recursive_factorial` function tail recursive:

```python
def recursive_factorial(n):
    def helper(n, k):
      if n == 1 or n == 0:
          return k
      else:
          return helper(n - 1, k * n) # This call to helper is the last call of the whole function
    return helper(n, 1)
```

This function above does the same thing as the `recursive_factorial` function we did above, except this is now tail recursive. Notice how we needed a helper function to store the eventual value? Other than that though, it's a very similar solution. The only real difference comes in the recursive case.

```python
return helper(n - 1, k * n)

return n * factorial(n - 1)
```

In the first example, `helper(...)` is the last call, while in the second example, the last call is actually `n * ...`, making the second one not in a tail context.

Linear recursive functions (aka not tree recursive functions) can pretty often be rewritten to be tail recursive, allowing them to be ran pretty efficiently in Scheme. (Python doesn't have tail recursion built in.)

### Examples: Are they tail recursive?

```scheme
;; Compute the length of s.
(define (length s)
    (+ 1 (if (null? s)
        -1
        (length (cdr s))) ) )
```

{{<details title="Answer" open=false>}}
No because the `if` statement is not in a tail context (the last recursive call in the function is `+ 1`)
{{</details>}}

```scheme
;; Return whether s contains v.
(define (contains s v)
    (if (null? s)
    false
    (if (= v (car s))
        true
        (contains (cdr s) v))))
```

{{<details title="Answer" open=false>}}
Yes because the `if` statements are all in tail contexts
{{</details>}}

Hopefully these examples are enough to get you to understand what a tail recursive function is.

# Trampolining

Python doesn't have its own native way of dealing with tree recursive functions - however, we can implement this in Python using trampolining (which also happens to be how you implement tail recursion in the Scheme project)

## Thunks

Don't ask me why they're called thunks; I have absolutely no idea at all and do not intend to know either.

Thunks are expressions that are wrapped in argumentless functions:

```python
thunk1 = lambda: 2 * (3 + 4)
thunk2 = lambda: add(25, 25)
```

You can then call this thunk later by just calling these functions `thunk1()`, `thunk2()`

## Process of making a trampolining function

When you make a trampoline, you essentially need to make a loop that **iteratively** invokes these thunk-returning functions.

```python
def trampoline(fn, *args):
    thunk = fn(*args)
    while callable(thunk): # checks whether it's still a function (essentially)
        thunk = thunk()
    return thunk

def recursive_factorial(n):
    def helper(n, k):
      if n == 1 or n == 0:
          return k
      else:
          return lambda: helper(n - 1, k * n) # This call to helper is the last call of the whole function
    return helper(n, 1)

trampoline(recursive_factorial, 3) # 6
```

Because our `recursive_factorial` function returns lambda values, we are able to exit out of these functions, allowing for our code to not run under a stack overflow.

In the Scheme interpreter, you won't make thunks with lambda functions but instead with classes, and then check whether they're still callable using `isinstance`. The concept is still very similar though - try and see if you can apply it to the question.


