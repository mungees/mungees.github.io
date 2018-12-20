---
layout: post
title: Tail-recursive functions
description: ""
tags: [functional programming]
categories: [TIL]
---

When functions are called, they are usually stored on the call stack, a part of memory, and the size of the call stack matters when it comes to a recursive function. Here is a function that returns a sum of numbers at a given number n such that `sum = n + (n-1) + (n-2) ... 0` in which the number of function calls is O(n).

```racket
; this is an example in racket version
(define (sum n)
    (if (= x 0)
        0
        (+ x (sum (- n 1)))))
```

The above function will evaluate in this way.

```
sum(5)
5 + sum(4)
5 + (4 + sum(3))
5 + (4 + (3 + sum(2)))
5 + (4 + (3 + (2 + sum(1))))
5 + (4 + (3 + (2 + 1)))
15
```

If the large nubmer is fed, then the call stacks will be filled up quickly and eventually raise a Runtime error.

Then, how can we tackly this problem? Use `acc`!

```
(define (sum n)
    (define (sum-helper n acc)
        ; just simply return acc when n becomes 0
        (if (= n 0)
            acc
            (+ acc (sum-helper (- n 1)))))
    (sum-helper n 0)
```

Now, look at the call stacks below. 

```
sum-helper(5, 0)
sum-helper(4, 5)
sum-helper(3, 9)
sum-helper(2, 12)
sum-helper(1, 14)
sum-helper(0, 15)
15
```

In functional programming, the tail-recursive way is a key technique so it is very important to practice converting recursive functions to tail-recursive functions.
