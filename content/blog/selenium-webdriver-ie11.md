---
title: "Selenium WebDriver and IE11"
date: "2017-11-22"
cover:
  image: "/images/blog/internet-explorer-11.jpeg"
summary: "Enable Protected mode on IE 11"
---


I was running Selenium WebDriver 3.5 on Windows 8.1 and using Internet Explorer 11. The test was just opening the Google web page. Internet Explorer opened correctly and displayed the Google page but then the test failed with the error:

```
OpenQA.Selenium.NoSuchWindowException : Unable to get browser
```

It turns out this is an [issue with Internet Explorer 11 rather than the InternetExplorerDriver](https://code.google.com/p/selenium/issues/detail?id=6511). This causes the InternetExplorerDriver to lose the connection to the instance of Internet Explorer it created.

## All security zones should be set to the same Protected Mode setting

I found that setting the Local Intranet zone's `Enable Protected Mode` setting to true solved my problem for me.

1. Press the `Alt` key to bring up the IE11 menu bar.
2. Select `Tools > Internet Options` and go to the `Security` tab.
3. Select each zone (Internet, Local intranet, Trusted sites, Restricted sites) and check the `Enable Protected Mode` check box.
