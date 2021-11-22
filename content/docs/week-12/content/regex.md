---
title: "RegEx"
weight: 3
draft: true
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# RegEx (Regular Expression)

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
RegEx|Pattern matching strings
BNF|Parsing strings into syntax trees (+ defining the syntax of a language)
SQL|Querying and Modifying database tables

# Regular Expressions - Explanation

## Pattern Matching

Quite often you might need to match certain patterns in a string (for example seeing whether something is an email).

This is far easier with a declarative approach (using RegEx) than using an imperative approach. Let's look at an example:

### Imperative

```python
def is_email_address(string):
    parts = string.split('@')
    if len(parts) != 2:
        return False
    domain_parts = parts[1].split('.')
    return len(domain_parts) >= 2 and len(domain_parts[-1]) >= 2
```

### Declarative

```python
r"(.+)@(.+)\.(.{3})" # RegEx approach
```

You won't understand the RegEx approach yet - that's completely fine. But notice how much shorter (and more general) the declarative approach has? It solves for a specific domain, so it's far easier to write code for it as long as you learn its syntax.

## Matching Exact Strings

> Make sure to use [regex101](https://regex101.com/)! It's very very very helpful to figure out what RegEx strings to put down

In RegEx, you can *match* exact strings by simply typing the string you want to match. One caveat is that RegEx has special characters reserved that you will need to *escape* to use in your exact matches. The following characters are characters you have to escape to use in an exact match: `\`, `[`, `]`, `(`, `)`, `{`, `}`, `+`, `*`, `?`, `+`, `$`, `^`, `.`, etc.

To match a string that has no special characters, just type the string itself. However, if the matched string contains any of the special characters mentioned above, make sure to escape them using a backslash (`\`).

For example: `r"\(1 \+ 3\)"` - we need to escape `(`, `+`, and `)`.

These examples are pretty useless though - RegEx can get significantly more powerful.

## The Dot

The `.` character matches every single character that is not a new line. (This could be either letters or numbers or really anything)

While this by itself doesn't seem particularly useful, it becomes far more useful in conjunction with other quantifiers.

## Character Classes

