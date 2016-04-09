---
layout: post
title:  "cocos2d-x, TextField, Hide keyboard(IME)"
date:   2016-04-10 00:13:00 +0900
category: cocos2d-x
tags: [c++,TextField]
---

Below code don't work to hide keyboard
``` cpp
_textField->setDetachWithIME(true);      //(X)
```


So I use other way like
``` cpp
static_cast<CCTextFieldTTF*>(_textField->getVirtualRenderer())->detachWithIME();    //(O)
```