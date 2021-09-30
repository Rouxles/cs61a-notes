---
title: "Trees"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Trees

A **tree** is an abstract data structure (basically not implemented by default in Python), which means we need to use **data abstractions** in order to implement this structure.

## What does a tree look like?

A tree has a **root** and a list of **branches**, where each branch is a tree itself.

![tree drawing](https://i.imgur.com/eqFLbBb.png)

A tree with zero branches (the white circles in the drawing above) is called a `leaf`. A tree also starts at the root, which in the drawing above, is the blue circle.

{{<hint info>}}
While this may not look like a tree, but rather roots of the tree itself, you could potentially think of the drawing as an upside down tree.
{{</hint>}}

Also notice how when we look at the branches stemming from the root, we have two separate sub-trees? This means that **recursion** will be a common way to go about solving tree-related problems.

---

Each location in a tree can be called a `node`, and each node has a `label` which contains the value located within the node (can be any value). Nodes can be parents/children of each other, and the top node is the `root` node.

## Tree Data Abstraction

There are many possible data abstraction for trees, but the one that CS61A uses is the following:

Abstraction|Description
:--|:--
`tree(label, branches = [])`|Returns a tree with root `label` and a **list** of `branches`
`label(tree)`|Returns the `label` of the tree
`branches(tree)`|Returns the branches of the tree (in a list) — each of which is a tree by itself
`is_leaf(tree)`|Returns `True` if the current node is a leaf node.

For example, a tree could be the following:

```python
t = tree(3, # Root Node
            # Branches:
            [tree(2, [tree(1)], # Left Branch
            tree(4))] # Right Branch
        )
```

The actual implementation of the tree is information that you do not need to know in order to use this data structure, so I will not write the implementation here. The documentation for these data abstractions says that `branches(tree)` returns a **list**, meaning that calling `branches(tree)[0]` is not a violation of data abstraction here.