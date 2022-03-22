---
title: "Midterm 2"
weight: 3
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Midterm 2

This is (in my opinion) the hardest test that you're going to take in this class simply because of the wide scope of content that you're expected to know, despite much of the content (for example linked lists, trees, quite a bit of OOP) being fairly new. It certainly doesn't help that much of the newer concepts heading into the second midterm tend to be more abstract and slightly difficult to grasp.

Once again, starting early is key (similarly to what it was like with midterm 1), but in particular for concepts such as OOP and recursion in general - make sure you truly understand what you're doing in HW/Lab/Discussion on a conceptual level: just seeing that all the test cases pass does not mean that you understand everything.

There's going to be a bit of conceptual guides in the sections below, but don't rely on this as your only source of understanding. Instead, come up with your own way of thinking and making sure that you truly understand what you're doing.

## Getting used to keeping track of objects

One thing I strongly recommend is drawing a diagram to help yourself keep track of objects rather than trying to do it all in your own head. It seriously makes dealing with objects far easier, especially when the questions get needlessly complicated like they do in CS61A. Keeping track of things using a diagram allows you to sort of more mindlessly go through the questions by basically doing the same thing every time, which will greatly help with your consistency with OOP questions, but more importantly, also help out with exam nerves (because there's far less to keep track of, even though you do need to take slightly more time to prepare)

## Environment diagrams with mutation

Similarly to OOP questions, you can also see a bunch of instances of list mutation in questions, except for lists themselves, the skill for drawing environment diagrams for lists can actually be tested. As a result, I strongly recommend getting used to environment diagrams (if you haven't gotten used to them already) because they seriously help with understanding the way lists work in Python (and kind of also gives you an insight on how things work in other languages too, cause in general, they're pretty similar to other languages)

## Getting comfortable taking the recursive leap of faith

In general, the idea of taking the recursive leap of faith is super abstract, so I'll try to break it down in the way that my mind likes to think of it (this is *not* going to work for everyone, but hopefully this perspective can at least help some other people gain a better understanding of what this recursive leap of faith thing actually means).

In general, when I write a recursive solution, I always think of it as having 3 different steps: the base case, the recursive call (aka the leap of faith), and connecting it all together. I'll talk about the first and the third step in a bit, but the recursive call is probably the hardest one to grasp. One instinct that I had when I first took the course was to trace through each recursive call and see what would eventually happen. While this approach works at the start for somewhat simpler recursive problems, it will quickly get really hard to keep track of when questions get complicated.

The idea of the recursive leap of faith is that you don't really need to trace through the whole function, but you just write the function with the assumption that your recursive call gives you the answer you expect. As long as you write everything else correctly (which by the way is just base cases and connecting things together), this assumption is guaranteed to hold true, and give you a correct recursive solution.

If that sort of idea doesn't make too much sense at the moment, the video below might help (this question is very difficult, so it's not really the best idea for *learning* recursion, but that's what the other section I wrote is for.)

- [Video](https://youtu.be/abvuh4Bd0nI)
