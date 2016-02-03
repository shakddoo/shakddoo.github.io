---
layout: post
title:  "android.os.NetworkOnMainThreadException"
date:   2016-01-18 22:00:00 +0900
category: Exceptions
tags: [Android, Network, Thread]
---

#1.Exceptions
- **android.os.NetworkOnMainThreadException**
- This Exception is happend when your android api version is upper 3.0(honeycomb) and network processing on Main-Thread. After Honeycomb, Google restric using network api on Main-Thread.

#2. Solutions
  If you have to use network api, handle on background thread.