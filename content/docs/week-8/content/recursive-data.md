---
title: "Recursive Data"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Recursive Data

## Linked Lists

Python lists are implemented in a way that makes inserting and deleting from the front of a list very inefficient. This is because Python implemented a list such that the first element of the list is always at the same memory location and elements in a list are located right next to each other, so when something is inserted to the start, everything gets pushed forward by one space in memory to make space for an element. 

If you ever need to constantly add to the front of a list, a Python list may not be a good idea. That's where a Linked List can come in handy.

Imagine building a list where each element can be anywhere in memory, and all that needs to happen is that one element knows where the next is:

![](https://i.imgur.com/eDYdRlh.png)

I drew each node (or element) in a different location on the page just to illustrate that these blocks could be anywhere on the page and do not need to be directly next to each other like in a list. Each instance/element/node of our linked list just needs a value inside it, and an arrow pointing to the next linked list object. If we think of it this way, we can construct our own Linked List class.

```python
class Link:
    empty = () # How we will refer to an empty linked list
    def __init__(self, first, rest = empty):
        self.first = first
        self.rest = rest
```

Using this class, we can then define our first linked list!

```python
my_link = Link(1, Link(2), Link(3)) # Notice how similar it is to the tree data abstraction you used earlier
```

In the example above, `1` is what gets stored in `self.first`, while `Link(2, Link(3))` is what gets stored in `self.rest`, meaning that we are able to continue accessing our linked list.

However, you can notice one thing straight away! 

## Link Class

A fancier version of the linked list that CS61A uses is the following:

```python
class Link:
    """A linked list."""
    empty = ()

    def __init__(self, first, rest=empty):
        assert rest is Link.empty or isinstance(rest, Link) # makes sure that the rest is either a linked list or emtpy
        self.first = first
        self.rest = rest

    def __repr__(self):
        if self.rest:
            rest_repr = ', ' + repr(self.rest)
        else:
            rest_repr = ''
        return 'Link(' + repr(self.first) + rest_repr + ')' # Returns the link class

    def __str__(self):
        string = '<'
        while self.rest is not Link.empty:
            string += str(self.first) + ' ' # Recursion!!!
            self = self.rest
        return string + str(self.first) + '>'
```

## Tree Class