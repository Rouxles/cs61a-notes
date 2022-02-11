---
title: "Midterm 1"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Midterm 1

Welcome to your first CS61A Midterm! Please start revising early - it's a lot better spreading out your study over multiple days than to cram it all right before the exam. You'll learn more and more importantly, remember more (even in long term memory), setting you up to succeed more in future exams.

## Studying Tips

{{<hint info>}}
Most of the information in this section can be found on [CS61A's article on how to study](https://cs61a.org/articles/studying/).
{{</hint>}}

While studying, make sure to do so actively - don't just read the textbook, but instead, do past exam questions, make cheat sheets (more on this later)/flashcards/mnemonic devices (not really necessary in CS61A imo), or maybe even take notes on the Midterm 1 guide and make sure you know exactly what you have going into the exam itself.

Also, one thing I did to prepare for all my CS61A exams was the Josh Hug method. I found a small study group (I think 3 to 5 is a pretty good number to strive for), then met bi-weekly (weekly when closer to exams). In this process, we assign questions for **everyone** to do, and for each question, assigned one person to go through their solution and their thought process to the problem, allowing everyone to interject at any time. This process helps a lot especially when it comes to getting the hang of solving exam style questions.

## CS61A Specific Tips

Quite a lot of CS61A exams come down to pattern matching. While the exam questions aren't going to be identical to past exams (for obvious reasons), getting used to solving exam questions can really help you develop the thinking needed to solve CS61A problems. Try to do as many past exams as possible once you understand the foundations of this class to a somewhat decent level, just get started on exam questions right away. 

The next few sections will talk about what's more important to focus on as well as give examples on how to solve certain things.

### Reading the Question

*Please* spend time and read the questions. The questions + doctests give off so much information in these midterms to the point where it's a pretty terrible idea to just start solving the questions without doing anything beforehand.

When looking at questions, I tend to read the small description first and try to understand what the question is asking, then look at the doctests to see if my understanding matches what the doctests say. Afterwards, I look at the inputs the functions take, and mark down (next to the letters) what to expect and shift my mindset accordingly. Afterwards, I'll look at the code template (if there is one) and see what they give - whether it be temporary variables or certain lines (and indentations) and then try to understand what the possible things are to put in the question itself. Only after I have all this information is when I begin filling in the details of the question.

#### Example: Fall 2021 `3a`

- [Question](https://cs61a.org/exam/fa21/mt1/61a-fa21-mt1.pdf)
- [Video Link to Solution](https://www.youtube.com/watch?v=lWmRer4dBnM)

This question in particular is very useful to practice making sure that you know exactly what the behaviour of the function is intended to be. This can be done both by looking at the description of the question itself or looking at the doctests (given that there are enough of them to really showcase the edge cases of the functions).

In this question, you have a small note saying that we want to return the first element in the sequence if *more than one element has the same smallest `measure` value*, and this is reflected in the 5th doctest where they give an example of what to return when two numbers have the same `measure` value. 

### Environment Diagrams

One incredibly important thing to get used to in this class is environment diagrams. I'd argue that they're the most important thing you want to know to succeed in this class is environment diagrams. While they aren't particularly useful outside CS61A, they're very helpful in terms of understanding what Python does under the hood, and also helps you navigate the waters of the confusing variable names in CS61A.

A good thing about getting very comfortable with environment diagrams is that the questions cannot get complicated. When you see something in Python that seems weird at first, you will know exactly what to expect if you understand the rules of environment diagrams (there aren't a lot to remember; I'd also recommend avoiding rote learning these rules because they're super helpful to remember properly for future midterms).

#### Example: Fall 2019 `pumbaa`

- [Question](https://cs61a.org/exam/fa19/mt1/61a-fa19-mt1.pdf)
- [Video Link to Solution](https://youtu.be/74JI8aGKHVg?t=1078)

This was probably the hardest environment diagram question I had done to this point, so I'd **highly** recommend giving this a try and actually understanding how to do it, because this is the sort of question that makes other WWPD questions incredibly simple in comparison. If you want an approach on how to do this question, you can take a look at the video solution by course staff

### Understanding Lambda Expressions and Higher Order Functions

The next most important part for MT1 is understanding how to deal with higher order functions (HOFs). HOF questions are the ones that can get the most complicated (unless recursion has already been introduced by the time MT1 rolls around), and this can be made even more complicated with `lambda` functions in the mix.

#### Example: Fall 2021 `3c`

- [Question](https://cs61a.org/exam/fa21/mt1/61a-fa21-mt1.pdf)
- [Video Link to Solution](https://www.youtube.com/watch?v=WeYircZodQc)

This question looks pretty simple on the surface, and it kind of is as long as you really understand what the functions you coded earlier in the exam actually do. However, this can be a bit complicated because of the lambda function that needs to be used in part of the question. Try doing this for yourself and then seeing if the question makes sense - the process of coming with lambda functions is usually pretty similar to the process explained in the video.

#### Example: Fall 2021 `3d`

- [Question](https://cs61a.org/exam/fa21/mt1/61a-fa21-mt1.pdf)
- [Video Link to Solution](https://www.youtube.com/watch?v=KFQr8HySUcs)

This question can get pretty complicated, and much of it is because of the HOF-style thinking that you need. This way of thinking is pretty hard to explain in words, so if whatever I write here doesn't make too much sense, please watch the video that I'll attach alongside the solutions above, and hopefully that will make everything a bit more clear.

### Practice Practice Practice

The most important thing about CS61A is practice. You'll get used to the concepts more when you practice more questions.

---

You got this!
