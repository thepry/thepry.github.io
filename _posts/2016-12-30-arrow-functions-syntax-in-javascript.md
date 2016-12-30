---
layout: post
title:  "Arrow functions syntax in javascript"
date:   2016-12-30 4:00
categories: javascript
permalink: /arrow-functions-syntax-in-javascript
excerpt: Arrow function syntax in javascript is incredibly weird and inconsistent
---

# Preface

I was surprised by how incosistent and weird es6 arrow functions syntax is. I have counted *twelve* different ways of creating arrow function. Check this out:

```javascript
// Parentheses are required if there are no parameters
() => 'foo' // 'foo'
() => { return 'foo' } // 'foo'
() => {} // undefined
() => ({ foo: 'bar' }) // { foo: 'bar' }

// Parentheses are optional if there is only one parameter

x => 'foo' // 'foo'
x => { return 'foo' } // 'foo'
x => {} // undefined
x => ({ foo: 'bar' }) // { foo: 'bar' }

// Parentheses are required if there are more that one parameter

(x, y) => 'foo' // 'foo'
(x, y) => { return 'foo' } // 'foo'
(x, y) => {} // undefined
(x, y) => ({ foo: 'bar' }) // { foo: 'bar' }
```

# Summary

On the left side:

1. Parentheses are required if there are no parameters
2. Parentheses are optional if there is only one parameter
3. Parentheses are required if there are more that one parameter

On the right side:

1. Braces and `return` are optional if there's only one expression
2. Braces and `return` are required if there's more than one expression
3. Braces are required if function does nothing (or returns undefined)
4. Braces and `return` are optional if there's one expression which returns object. But object should be put into Parentheses.

There are 7 rules and 12 combinations and you will probably have to remember them all to read and write arrow functions. This is wrong.

Why can't we have one way of creating a function? Like we have with regular functions? Why not take the regular function syntax and replace `function` with `=>`?

```javascript
function(...){...}
// should have just become this
(...) => { ... }
```

# Always use the "full" syntax

Only the full version of arrow function syntax can be used in any situation. So I think we should configure linter to
allow only `(...) => {...}` syntax in our applications. For the sake of consistency!
