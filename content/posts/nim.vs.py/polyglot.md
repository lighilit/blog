+++
date = '2025-09-08T20:03:11+08:00'
draft = false
title = 'Polyglot'
+++

While [nimpylib](https://nimpylib.org)([repo](
https://github.com/nimpylib/nimpylib))
is handy to write Python code in Nim,

what if writing polyglot code,
which is runnable in both Nim and Python?

> [An example (NPython's test_decimalAndSpace.nim)](https://github.com/nimpylib/NPython/blob/5dffaea5daef781fb55154e7768ea614af08d113/Modules/unicodedata/test_decimalAndSpace.nim) using such polyglot
---

## How to
We simply write two parts:
- run in both languages (thanks to their similar syntax)
- snippets run in only one, ignored by another

Many parts of syntax of they two are similar, so we don't
discuss such here

and what's more important is that
how to make some code ignored by specified one language

### Cheat Nim to ignore some Python code
Let's start with the easier one.

```Python
#[
<Python code here>
[
]#
```

### Explain
Python regards it as:
- Comment `[`
- `<Python code here>`
- An empty list literal `[]`
- Comment `<empty>`

But in Nim `#[` starts a multiline comment and `]#` ends it.

### Restriction
No more needed to mention but
the restriction is `<Python code here>` cannot contain `]#`.

If any, simply rewrite as `] #` like `[1,2,3] # xxx`

### Cheat Python to ignore some Nim code
This part is harder.

I'd like to give my solution:

### steps

```Nim
"""\""".`!=`("").assert
<Nim code here>
discard "" != """"_"""
```

> You can also use `assert` over `discard` on the last line, which is easier to remember.

### Restriction
The only restriction is that `<Nim code here>` cannot contain `"""`.

If any, ...consider to split into single line string literals.

#### Explain
This trick takes advantage of some difference between Nim and Python when
parsing multiline string literal node.

Here are their parsing results:

##### Nim:

->

```Nim
assert "" != ('\\' & '"')
<Nim code here>
discard "" != ('\\' & '_')
```

dumpTree:

```
  Command
    Ident "assert"
    Infix
      Ident "!="
      StrLit ""
      TripleStrLit  "\\\""  # `\"`
  <Nim code here>
  DiscardStmt
    Infix
      Ident "!="
      StrLit ""
      TripleStrLit  "\"_"   # `\_`
``` 

##### Python:

->

```Python
"""\""".`!=`("").assert
<Nim code here>
discard "" != """ "_" ""
```

->

```Python
"""\""".`!=`("").assert
<Nim code here>
discard "" != _"""
```
->

```Python
'''""".`!=`("").assert
<Nim code here>
discard "" != _'''
```
