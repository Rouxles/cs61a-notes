---
title: "Environment Diagrams"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Environment Diagrams

Environment Diagrams are a good way to visualize how Python deals with its execution, and can also help you to visualize how more complicated pieces of code (e.g. Higher Order Functions) work.

[PyTutor](https://pythontutor.com/composingprograms.html#mode=edit) has a way of converting from code to environment diagrams, so please use that as a resource! The diagrams below are not going to match those from PyTutor exactly due to `Markdown` constraints, but I will try to emulate them as well as possible.

## Variable Assignment

```python
x = 2
y = 5
```

When the code block above is run, the value `2` will be assigned to the name `x`, and afterwards, the value `5` will be assigned to the name `y`, which can be seen in an environment diagram like the one below:

{{< mermaid>}}
    graph LR;
    subgraph Global Frame
    x --- 2
    y --- 5
    end
{{< /mermaid >}}

In each `frame`, there can only be one name bound to one value - it is not possible to have one name point to two different values.

## Function Assignment

Functions are notated differently to variables due to the potential need to overwrite a binding without losing the value of a function somewhere else (will make sense later).

```python
def square(n):
    return n*n

square(3)
```

This will be executed in two different steps: creating the function, then executing the function.

```python
def square(n):
    return n*n
```

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    square --> id1["func square(x) [parent = Global]"]
    end
{{</mermaid>}}

```python
square(3)
```

When a function is called, a **new frame is created**, leading to another environment for Python to execute code from. Note that an environment variable only needs the **function name, parameter(s), and parent frame** in the environment diagram.

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    square --> id1["func square(x) [parent = Global]"]
    end
    subgraph "f1: square [parent = Global]"
    n --- 3
    id2[Return Value] --- 9
    end   
{{</mermaid>}}

As can be seen in the environment diagram above, a new unique frame `f1` is created, which has all the passed in parameters (in this case, just `n = 3`) stored. Then, when the return statement is reached, it simply evaluates the right side of the return statement (in this case `n*n`), then returns that value (`9`)

### Confusing Function Assignment Example

(Taken from Fall 2021 Discussion 1)

```python
def double(x):
    return x * 2

def triple(x):
    return x * 3

hat = double
double = triple
```

The functions `double` and `triple`'s environment diagrams are pretty self-explanatory, but the next two statements `hat = double` and `double = triple` are slightly more confusing. Let's break it down:

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    triple --> triple_function["func triple(x) [parent = Global]"]
    end
{{</mermaid>}}

What would happen with `hat`? In this case, it points to the function `double(x)` rather than the name `double` itself. This means that `hat` becomes a **copy of** `double` rather than acting as `double`. Take a look at the environment diagram below:

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    triple --> triple_function["func triple(x) [parent = Global]"]
    hat --> double_function
    end
{{</mermaid>}}

Both `double` and `hat` point to the same function `double(x)`!

Now, what would happen with `double = triple`? You can simply extrapolate the actions above, but quite simply, the pointers change.

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> triple_function
    triple --> triple_function["func triple(x) [parent = Global]"]
    hat --> double_function["func double(x) [parent = Global]"]
    end
{{</mermaid>}}

This means that you can still call the `double(x)` function through `hat`, but you can no longer call it through `double`. Additionally, even when `double` was overwritten, the function `double(x)` itself was not deleted!

## Call Expressions

The important thing to note is that when executing call expressions, a new frame is created to keep track of local variables. The order of operations is as follows:

1. Evaluate the operator - this should evaluate to a function.
2. Evaluate the operands from left to right.
3. Make a new frame with:
   1. A **unique** index
   2. The real name of the function (not the name of the variable pointing to it) (for example, for `double(n)`)
   3. The parent frame
4. Bind values to names in this new frame.
5. Evaluate the function in this new frame until a return value is obtained.

Example from Fall 2021 Discussion 1:

```python
def double(x):
    return x * 2

hmmm = double
wow = double(3)
hmmm(wow)
```

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    hmm --> double_function
    end
{{</mermaid>}}

After the function `double(x)` is bound to a name, and `hmm` is bound to that function, we create a new frame to evaluate `wow = double(3)`.

When evaluating that statement, the right side is evaluated before being assigned to the name on the left side. As a result, `wow` will not appear in the environment diagram until **after** the return value is created.

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    hmm --> double_function
    wow -- "(After the return value below is evaluated)" --- outer[6]
    end
    subgraph "f1: double(x) [parent = Global]"
    x --- 3
    return[Return Value] --- 6
    end
{{</mermaid>}}

Afterwards, `hmmm(wow)` is called, which is essentially the same thing as doing `hmmm(6)`. As `hmmm` is pointing to `func double(x) [parent = Global]`, it will run that function, passing in the parameter `6`. However, because this is a new function, a new frame will be created.

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    hmm --> double_function
    wow -- "(After the return value below is evaluated)" --- outer[6]
    end
    subgraph "f1: double(x) [parent = Global]"
    x --- 3
    return[Return Value] --- 6
    end
    subgraph "f2: double(x) [parent = Global]"
    f2-x[x] --- f2-6[6]
    f2-return[Return Value] --- f2-return-value[12]
    end
{{</mermaid>}}

### Nested Call Expression

Environment diagrams can also help visualize how to deal with nested call expressions.

For example:

```python
def double(x):
    return x*2

result = double(double(2))
```

How would this look in an environment diagram?

First, the inner `double(2)` gets evaluated, so a frame is created for that, then the return value from that is used in the outer function, so another frame is created for that.

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    end
    subgraph "f1: double(x) [parent = Global]"
    f1-x[x] --- f1-2[2]
    f1-rv[Return Value] --- f1-r[4]
    end
{{</mermaid>}}

After the inner function is evaluated, the return value is then passed into the function to be run again in another frame:

{{<mermaid>}}
    graph LR;
    subgraph Global Frame
    double --> double_function["func double(x) [parent = Global]"]
    end
    subgraph "f1: double(x) [parent = Global]"
    f1-x[x] --- f1-2[2]
    f1-rv[Return Value] --- f1-r[4]
    end
    subgraph "f2: double(x) [parent = Global]"
    f2-x[x] --- f2-4[4]
    f2-rv[Return Value] --- f2-r[8]
    end
{{</mermaid>}}

{{<hint info>}}
**Note:** Both of the parents of the function are the global frame because the function itself is called, and that is located inside the parent frame.
{{</hint>}}

## Names in Environments

Names have different meanings in different environments!

```python
def double(double):
    return double + double

double(2)
```

**Please do not write code like this.** It is merely a demonstration of how names and environments interact. 

{{<mermaid>}}
graph LR;
subgraph Global Frame
global_double[double] --> glob_double_function["func double(double) [parent = Global]"]
end
subgraph "f1: double(double) [parent = Global]"
f1_double[double] --- 2
f1_r[Return Value] --- 4
end
{{</mermaid>}}

Notice how the different environment frames allow for the name `double` to exist twice with different assignments.

## Environment Diagrams for Higher-order Functions

Note that functions are **first class** in Python - they act the same as values.

### HOF: Takes a function as an argument

```python
def run_twice(func, *args):
    return func(func(*args))

def double(x):
    return x*2

double_double = run_twice(double(2))
```

What `*args` does here is simply allow for a flexible number of arguments to be passed in rather than a set number - allows for more flexibility even though it doesn't do much here.

{{<mermaid>}}
graph LR;
subgraph Global Frame
global_run_twice[run_twice] --> global_run_twice_function["func run_twice(func, *args) [parent = Global]"]
global_double[double] --> global_double_function["func double(x) [parent = Global]"]
end
{{</mermaid>}}

After assigning the functions to the names, we get the environment diagram seen above. To evaluate `double_double = run_twice(double(2))`, you have to remember the order of operations for call functions. First, evaluate the operators (make sure it exists/is not a higher order function), then evaluate the operands, then apply the operator to the operands.

In this context it means that `run_twice` is evaluated first with the proper pointers, then `double` is run after that is done.

{{<mermaid>}}
graph LR;
subgraph Global Frame
global_run_twice[run_twice] --> global_run_twice_function["func run_twice(func, *args) [parent = Global]"]
global_double[double] --> global_double_function["func double(x) [parent = Global]"]
end
subgraph "f1: run_twice(func, *args) [parent = Global]"
f1_func[func] --> global_double_function
f1_args[args] --- 3
end
subgraph "f2: double(x) [parent = Global]"
f2_x[x] --- f2_3[3]
f2_r[Return Value] --- 6
end
{{</mermaid>}}

Afterwards, we get the following:

{{<mermaid>}}
graph LR;
subgraph Global Frame
global_run_twice[run_twice] --> global_run_twice_function["func run_twice(func, *args) [parent = Global]"]
global_double[double] --> global_double_function["func double(x) [parent = Global]"]
global_double_double[double_double] --- global_12[12]
end
subgraph "f1: run_twice(func, *args) [parent = Global]"
f1_func[func] --> global_double_function
f1_args[args] --- 3
f1_r[Return Value] -- "(Only after f3's return value is evaluated)" --- f1_rv[12]
end
subgraph "f2: double(x) [parent = Global]"
f2_x[x] --- f2_3[3]
f2_r[Return Value] --- 6
end
subgraph "f3: double(x) [parent = Global]"
f3_x[x] --- f3-6[6]
f3_r[Return Value] --- f3_rv[12]
end
{{</mermaid>}}

These environment diagrams do get somewhat complicated.

### HOF: Nested Environment Diagrams

Notice how the parent for functions was always `Global`? Well with nested environment diagrams, you'll finally see a situation where the parent isn't always `Global`!

```python
def make_adder(n):
    def adder(x):
        return x + n
    return adder

add_3 = make_adder(3)
add_3(2)
```

{{<mermaid>}}
graph LR;
subgraph "f2: adder(x) [parent = f1]"
f2_n[x] --- f2-5[5]
f2_r[Return Value] --- f2-rv[5]
end
subgraph "f1: make_adder(n) [parent = Global]"
f1_n[n] --- 3
f1_adder[adder] --> f1_adder_f["func adder(x) [parent = f1]"]
f1_r[Return Value] --- f1_adder_f
end
subgraph Global Frame
g_make_adder[make_adder] --> g_made_adder_f["func make_adder(n) [parent = Global]"]
g_add_3[add_3] --> f1_adder_f
end
{{</mermaid>}}

After the code has finished executing, we can see that the environment diagram. There are some points to take note of.

#### Variable Finding Procedure

This was briefly mentioned in an earlier post, but the order is as follows:

1. Find name in local frame
2. If that could not be found, search one parent up and see if they have the name in that frame.
3. Repeat until there are no more parent frames. If nothing could be found, throw an error

Why is this important?

```python
def make_adder(n):
    def adder(x):
        return x + n # Important on this line
    return adder
```

As you can see, the variable `n` is not located within the actual code body of `adder`, meaning that the program would not be able to execute the function if it were only allowed to search from its local frame. `adder`'s parent is `make_adder` (and its parent frame is `Global`), meaning that when `adder` is run as a function, it can search for a specific variable in its own frame, its parent frame after that (`make_adder`), and the parent of its parent (`Global`)

Here's a good exercise to test your understanding (Taken from lecture 5 of Fall 2021):

```python
def thingy(x, y):
    return bobber(y)
        
def bobber(a):
    return a + y

result = thingy("ma", "jig")
```

What would be returned here?

Spoiler: It's an error. Why? Let's make an environment diagram.

{{<mermaid>}}
graph LR;
subgraph Global Frame
g_thingy[thingy] --> g_thingy_f["func thingy(x, y) [parent = Global]"]
g_bobber[bobber] --> g_bobber_f["func bobber(a) [parent = Global]"]
end
subgraph "f1: thingy(x, y) [parent = Global]"
f1_x[x] --- f1_ma["ma"]
f1_y[y] --- f1_jig["jig"]
end
subgraph "f2: bobber(a) [parent = Global]"
f2_a[a] --- f2["jig"]
end
{{</mermaid>}}

Notice how `f2` only has the variable `a` that it can access in its environment, and the variable `y` cannot be found within its own environment, nor can it be found in any parent after that (which in this case would just be `Global Frame`). As a result, this throws an error because a name could not be found.

## Self-Referencing Functions

A higher order function could return a function that references its own name. Take this for example:

```python
def print_sums(n):
    print(n)
    def next_sum(k):
        return print_sums(n + k)
    return next_sum

print_sums(1)(3)
```

This is quite complicated to read but understanding it is well worth the cost.

As you can see above, the `next_sum` function with parent `print_sums` returns `print_sums` itself, meaning that it's a function that references itself, hence being self-referential.

Let's try to make an environment diagram for that:

{{<mermaid>}}
graph LR;
subgraph Global Frame
g_print_sums[print_sums] --> g_print_sums_f["func print_sums(n) [parent = Global]"]
end
subgraph "f1: print_sums(n) [parent = Global]"
f1_n[n] --- 1
f1_next_sum[next_sum] --> f1_next_sum_f["func next_sum(k) [parent = f1]"]
f1_r[Return Value] --> f1_next_sum_f
end
{{</mermaid>}}

After `f1` has been evaluated, we can see that the return value of `f1` returns a function. Now looking at the `print_sums(1)(3)` statement, we can see that `print_sums(1)` evaluated to a function, meaning that you now have something equivalent to `next_sum(3)`, and the value of `n` in that function can be found by looking at its parent frame.

{{<mermaid>}}
graph LR;
subgraph Global Frame
g_print_sums[print_sums] --> g_print_sums_f["func print_sums(n) [parent = Global]"]
end
subgraph "f1: print_sums(n) [parent = Global]"
f1_n[n] --- 1
f1_next_sum[next_sum] --> f1_next_sum_f["func next_sum(k) [parent = f1]"]
f1_r[Return Value] --> f1_next_sum_f
end
subgraph "f2: next_sum(k) [parent = f1]"
f2_n[k] --- 3
end
{{</mermaid>}}

At that point, the function `print_sums` is called again, leading to this:

{{<mermaid>}}
graph LR;
subgraph Global Frame
g_print_sums[print_sums] --> g_print_sums_f["func print_sums(n) [parent = Global]"]
end
subgraph "f1: print_sums(n) [parent = Global]"
f1_n[n] --- 1
f1_next_sum[next_sum] --> f1_next_sum_f["func next_sum(k) [parent = f1]"]
f1_r[Return Value] --> f1_next_sum_f
end
subgraph "."
subgraph "f3: print_sums(n) [parent = Global]"
f3_n[n] --- 4
f3_next_sum[next_sum] --> f3_next_sum_f["func next_sum(k) [parent = f3]"]
f3_r[Return Value] --> f3_next_sum_f
end
subgraph "f2: next_sum(k) [parent = f1]"
f2_n[k] --- 3
f2_r[Return Value] -- "(Only after f3 finishes evaluating)" --> f3_next_sum_f
end
end
{{</mermaid>}}

As there are print statements in the function, there will also be something output to the console, which in this case is the following:

```python
1
4
```

Confusing? Sure, but it's important to be able to draw these environment diagrams to help visualize certain parts of code.

It's important to note that if another call were to be made after this function call, the parent of the next frame would be `f3` as there is updated information in the outer function.

## Currying

Currying takes a single function that takes multiple arguments and turns it into a higher-order function with single arguments.

Let's take a look at the differences between the following functions:

```python
from operator import add
add(2, 3) # two arguments

def make_adder(n):
    return lambda x: n + x

make_adder(2)(3) # higher order function with one argument in each
```

Above, `make_adder` is an example of `currying` `add(2, 3)`.

A way to curry a function with any two arguments can be done like this:

```python
def curryer(f):
    def g(x):
        def h(y):
            return f(x, y)
        return h
    return g
```

What this does allows only a single argument to be passed into the function each time (similarly to `make_adder`), but because of the rules of name lookup in Python, the variables `x`, `y`, and `f` can still be accessible from the innermost function. You can try inputting it into PyTutor, but for this one, it's a good exercise to try and draw it yourself before checking the answers.