---
title: "How to enable Firebug on newer versions of Firefox"
date: "2017-02-04"
cover:
  image: "/images/blog/firefox.png"
summary: "In the previous article, I’ve announced that Firebug is no longer supported in the latest versions of Firefox."
---

In the previous article, I've announced that Firebug is no longer supported in the latest versions of Firefox.

It is possible however to make it work again, by disabling the e10s (electrolysis) architecture of the browser. If you're ready to get rollin', proceed below:

### Guide:

1\. We need to change some config options first, so hit **about:config** in your URL address bar.

2\. Search for the **browser.tabs.remote.autostart.2** option and set the boolean value to False (check the screenshot below).

<Image
  alt={``}
  src={`/static/images/blog/disable-e10s.webp`}
  width={1000}
  height={600}
  priority
/>

3\. Now let's check if the option is correctly set by visiting **about:support** and check the value of the **Multiprocess Windows** field. It should be set to 0/1 right now.

<Image
  alt={``}
  src={`/static/images/blog/disable-value.webp`}
  width={1000}
  height={600}
  priority
/>

4\. Restart the browser and install & enable our beloved Firebug extension.

 

#### Notes:

\- You will have visible performance issues if you disable e10s.

\- This has been tested with Firefox version 51.0.1 (64bit), however it should work for later versions also.
