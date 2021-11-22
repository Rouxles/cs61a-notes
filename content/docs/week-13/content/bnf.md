---
title: "BNF (Backus-Naur Form)"
weight: 1
draft: true
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# BNF

## Declarative Languages vs Imperative Languages

RegEx is a declarative language, while Python is an Imperative language. What's the difference?

- Imperative languages
  - A program is a description of computational instructions
  - The interpreter/compiler carries out the execution as you tell it to - you (essentially) know how everything is implemented yourself
- Declarative languages
  - A program is a statement of the desired result
  - The interpreter will use its own algorithms to figure out how to generate the result it wants.

## Domain-specific

Most of the time, declarative languages are domain specific, meaning that they tackle specific problems. The three declarative languages that we will be looking at in this version of CS61A all have different domains.

Language|Domain
:--|:--
RegEx|Pattern matching strings (Won't be covered in this website - look at lecture slides for this because it's far more effective in that format)
BNF|Parsing strings into syntax trees (+ defining the syntax of a language)
SQL|Querying and Modifying database tables

# BNF - Explanation

## Describing Language Syntax

BNF was invented to describe a programming language. It's still used today for the exact same context (in fact, SQLite (will be covered later) documentation uses BNF in its documentation!)

A BNF grammar can be used for documentation or even a way to create a parser for a language.

## Basic BNF

BNF Grammar consists of two different things: terminal and non-terminal symbols. Conventionally, terminal symbols are those written in all capital letters while non-terminal symbols are in all lowercase letters.

Many things about BNF may remind you about recursion - try to get into that mindset when writing BNF grammar.

## BNF Example

Let's take a look at a simple grammar with just three rules:

```lark
?start: numbers 
numbers: INTEGER | numbers "," INTEGER
INTEGER: /-?\d+/
```

(In Python, we can build BNFs using the `lark` library - it's built in on [code.cs61a.org](https://code.cs61a.org))

For this library in particular, the grammar always starts with the `start?` symbol then branches off from there. In the example above, we will be able to parse strings like `3,2,1,6,4` and turn it into a syntax tree - you can see the result of that in code.cs61a.org. The `|` symbol functionally means the same thing as `or`

![](https://i.imgur.com/eqeDmsk.png)

## Defining Terminals

Terminals are something similar to base cases when it comes to recursion. In Lark grammar, we can write it with the following rules:

- Wrapping strings in `''` - does exact matches
- Regular expressions surrounded with `/` on both sides (e.g. `/\d+/`)

You might want to ignore any whitespace too because Lark treats it as a proper character. To do that, we just need to insert the line `%ignore /\s+/` to our Lark grammar.

## Repetition

Similarly to RegEx (if you don't know RegEx, please watch the lecture or use the more interactive lecture slides), you can use quantifiers to say whether stuff is required etc.

- `*`: 0 or more
- `+`: 1 or more
- `?`: 0 or 1

## Grouping

If you ever want to group certain things together, you can use parentheses:

```lark
NAME: /[a-zA-Z]+/
NUM: /\d+/
list: ( NAME | NUM )+
```

Wrapping something in `[]` makes that clause optional, for example with `numbered_list: ( NAME [ ":" NUM ] )+`.

