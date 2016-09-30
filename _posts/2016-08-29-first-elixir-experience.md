---
layout: post
title:  "First Elixir experience"
date:   2016-08-29 0:20
categories: elixir
permalink: /first-elixir-experience
excerpt: I started working on new project recently, which will require mobile app and some backend for it. I know Rails well enought and obvious choise would be to keep using it. But i wanted to learn something new so i decided to choose some functional language...
---

# Why Elixir?

I started working on new project recently, which will require mobile app and some backend for it. I know Rails well enought and obvious choise would be to keep using it. But i wanted to learn something new so i decided to choose some functional language. I needed some powerfull language with a nice syntax (i'm a big fan of ruby syntax), which i can start using easily. So i had to choose one of these:

- Haskell seems to be interesting language to learn, but not the one you would want to use in production. It's also requires some time to dive into it, and i needed result as soon as possible.

- Closure could be one of the option, but i'm scared of List.

- Scala seems to be too complex to start using it right away.

- Elixir was the best option. Firstly the sytax reminds me ruby, is really fast and good for parallel programming. Also Phoenix framework is a good production-ready clone of Rails. Elixir is getting trending nowadays and choosing it might be a good career choice as well.

# Syntax

Elixir's syntax is nice and consistent. For example you have to use `do` not only in your blocks but also in function and module definition.

```elixir
module MyModule do
  def my_func do
  end
end
```

I also like the pipe, which allows to ommit first parameter in multiple functions call:

```elixir
list = ["my string", "not mine string"]
list
|> List.first
|> String.reverse
# => "gnirts ym"
```

# Pattern matching

I had to rethink the `=` in Elixir. It's a pattern matching operation, not assigning. It's a very powerfull tool but sometimes might be confusing. Code like this:

```elixir
def my_func(value = :default_value) do
end
```

Will not assing `:default_value` to `value` if it's not specified. For default parameter value you have to use `\\`

```elixir
def my_func(value \\ :default_value) do
end
```

# No classes, no objects

Yes, Elixir is trully functional language, and you have only modules, functions and data structures. Instead of `[1, 2, 3].first` you call `List.first [1, 2, 3]`. Instead of modifying objects state you return new "modified" structure. Yes - structures, lists, tuples are immutable in elixir. But sometimes we need to work with state, right? And Elixir allows it offering you Erlang's actor model.

# Ecto library instead of ORM

I like Ecto, but i was hard to get used to it. The documentation is not as nice as Ruby docs, and sometimes it's at the beginning Ecto's syntax might be confusing. It prevents you from shooting in your foot, but requires you to write much more code than Active Record in Ruby. I'm not sure which I like more. Ecto seems more right way to work with db, but sometimes this explicity is annoying.

# Explicity vs Implicity

As I said above I don't know what I prefer: Implicit and full of magic Rails or Explicit Elixir way, which requires you to write more code. I understand that a lot in Rails world is wrong. Rails way is actually full of anti-patterns. But apart from that it allows you code fast and very efficiently, and get very nice and readable code as a result. Elixir seems to be less readable, just because you have more lines of code for same tasks.

# Documentation

The documentation sucks. Sometimes it's hard to understand how method works. I had a problem when my API worked fine in live, but didn't work in tests. And i couldn't find any info about that!

# Conclusion

Elixir is very good language, but using it has own pros and cons. Explicit code looks amazing in vacuum, but in real world it might be annoying and even confusing. The Phoenix framework works fine and some things are much better than in Rails: "plugs", modifying connection in all HTTP chain. Other things might be disputable.

I believe that in next few years Elixir community will add more documentation, write more libraries and Elixir will be one of the mainstream functional languages. It is powerfull, simple and easy to learn.

