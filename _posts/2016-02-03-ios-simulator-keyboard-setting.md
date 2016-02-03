---
layout: post
title:  "iOS Simulator keyboard is not shown"
date:   2016-02-03 22:04:00 +0900
categories: Exceptions
---

#1. Problem
cocos2d-x TextField,  keyboard is not shown on iOS Simulator.

#2. Solution
- iOS Simulator -> Hardware -> Keyboard
- Uncheck “Connect Hardware Keyboard”

![ios_simulator_keyboard_setting](https://shakddoo.github.io/images/ios_simulator_keyboard_setting.png)

You can see keyboard when you touch TextField area.

![ios_simulator_keyboard](https://shakddoo.github.io/images/ios_simulator_keyboard.png)
