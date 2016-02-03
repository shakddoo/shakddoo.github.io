---
layout: post
title:  "Selenium, protected mode settings are not the same for all zones"
date:   2016-01-30 01:00:00 +0900
category: Exceptions
tags: [Explore, Protected mode]
---

#1.Exceptions
- Unexpected error launching internet explorer. protected mode settings are not the same for all zones


#2. Solutions
- Explore->Option->Security tab
- Click on Security tab and make sure 'Internet','Local Intranet','Trusted sites' and 'Restricted sites' have 'Enable Protected Mode' either checked or unchecked for all options.
- Apply and save the settings and re-run the test code. It should work.