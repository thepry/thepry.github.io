---
layout: post
title:  "Integer nonsense"
date:   2016-12-08 0:20
categories: thoughts
permalink: /integer-nonsense
excerpt: Do we really need to use integers in modern high-level languages?
---

# Preface

*Please note that I'm speaking about high-level programming languages such as Ruby, Python, Javascript etc. I will use Ruby for examples*

As a developer I get used to the idea that there are different numbers in languages. We have Integer type for integer values, and Float/Decimal for numbers which have some decimal part. Like real numbers. But why do we need different number types?

There are few reasons to keep integers. First one - integers usually require less space than decimals. Second - integers represent numbers without a fractional component. And should always keep it that way. Or not?

What should happen if you have an operation like this: `3 + 0.5`?

In Ruby you will get `3.5` and your integer will be implicitly transformed to a float. I can understand logic behind this: we have a mathematical operation and result can not be represented with integer, so we have to use a float. So I guess we should get the float if we have something like this: `3 / 2`. But instead of `1.5` we will get the `1`. Of course we can find some logic in this as well. For example "If you have operation with integers, you will get an integer. If one of the numbers is a float you will get a float." But this sounds like an implicit hack.

Integers in Ruby require us to have special inconsistent math for them. Implicit type transormation.
Why `3 + 0.5` doesn't return `3`? Or maybe `4`? Or maybe it should raise an exeption, because we can not get a new integer out of these two numbers? Ruby has strong typing system but it doesn't work with numbers.

Is there something else special about integers? Well there is an idea of "next" number. `3` is followed by `4`, the next after `4` would be `5` and so on. You can not use `next` on `3.5` (but we can implement `next_int`)

Why don't we have just a Number, which would act like a number, use math for numbers and let us forget about different types of numbers? I don't want to care about how much space is required for storing my number, like I don't care about it when I use strings. I let the interpreter to deal with it. I want to think about entities, high-level operation and not bytes or cpu operations.
