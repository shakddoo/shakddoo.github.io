---
layout: post
title:  "Google Inapp Server Verification Error"
date:   2016-01-18 20:00:00 +0900
categories: Exceptions
---

#1.Exceptions
- google api accessNotConfigured 403error 
- The project id used to call the Google Play Developer API has not been linked in the Google Play Developer Console.

{% highlight json %}
{ "errors": [ { 
"domain": "usageLimits",
"reason": "accessNotConfigured",
"message": "Access Not Configured"
} ],
"code": 403, "message": "Access Not Configured" }}
{% endhighlight %}


#2. Solutions
**Google Developer Console**

*   **"Google Developer Console"** > "APIs & Auth" subcategory "APIs" > (api list) "Google Play Android Developer API". Set "STATUS" to "ON".
*   "APIs & auth" subcategory "Credentials" > "Create new Client ID". Choose "Service account" and create the id.
*   You should get a P12 key from the browser.  
  
<br/>

**Google Play Developer Console**

* **"Google Play Developer Console"** > "Settings" > subcategory "API access".
* Make a link to your "Linked Project".
* "Service Account" place maybe already showing ur "Service account" CLIENT ID which made "google developer console".