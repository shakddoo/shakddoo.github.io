---
layout: post
title:  "AttributeError: 'NoneType' object has no attribute '_root'"
date:   2016-01-31 02:00:00 +0900
category: Exceptions
tags: [python, StringVar]
---
###1. Exception
AttributeError: 'NoneType' object has no attribute '_root'


###2. Solution
StringVar needs a master

``` python
>>> StringVar(Tk())
```
or

``` python
>>> root = Tk()
>>> StringVar()
```
