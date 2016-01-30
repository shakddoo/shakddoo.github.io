---
layout: post
title:  "Python StringVar, AttributeError: 'NoneType' object has no attribute '_root'"
date:   2016-01-31 02:00:00 +0900
categories: Exceptions
---
#1. Exception
AttributeError: 'NoneType' object has no attribute '_root'


#2. Resolution
StringVar needs a master

``` python
>>> StringVar(Tk())
```
or
``` python
>>> StringVar(Tk())
```