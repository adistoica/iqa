---
title: "Automating Adobe Experience Manager with Hobbes.JS"
date: "2017-04-17"
cover:
  image: "/images/blog/hobbes.png"
summary: "Implementing a Test Automation framework for Testing Adobe Experience Manager using Hobbes.JS"

---
Since AEM 6.0, Adobe introduced a test automation framework called [Hobbes.JS](https://docs.adobe.com/docs/en/aem/6-0/develop/components/hobbes.html) that can provide functional automated tests for the AEM UI. The stock Hobbes.JS package from Adobe provides:

- A JavaScript API for creating tests.
- A Test panel in the touch-optimized UI for running tests.

Initially, we started to develop for one of our clients an automation framework based on Hobbes.JS that would provide us valuable results within the development process. From the beginning, we saw some advantages of using the Adobe tool because some facts were already proven like:

- Integration with AEM (only in author mode)
- Backend is based on JavaScript

![hobbes js in action](images/hobbes-png.png "hobbes js in action")

By seeing great potential in this tool, we saw the need to have **additional** features like:

- **Nightly** automated builds using [Jenkins](https://jenkins.io/)
- **Valuable** test reports, that can be used to provide a Quality Assurance health check to the client for each iteration. (JUNIT, Pretty and HTML formats)
- **Page objects** support – an organized way to organize the CSS locators in the development files
- **Slack** notifications – because our team needs to be constantly informed

**The Technical Datasheet**

Having our feature list ready, we have started development and after a few weeks of coding we are proud to introduce: **Hobbes Runner** – a Node.JS application that integrates directly with Hobbes.JS, extending it’s out of the box features.

The technical aspects of our wrapper can do the following:

- Hook in the Hobbes test process and act on various test events like: Start, Stop, Pause, Finish
- Extract test reports in XML, HTML and TXT formats to feed them to an external consumer like Jenkins (JUnit plugin)
- Specify the browser that will run (Firefox, Chrome or IE)
- Various debug levels for Selenium
- The ability to run in our  Selenium grid

And because a picture is worth a thousand words, check the screenshot below

![hobbes runner help file](images/word-image.png "hobbes runner help file")

**Developing with Hobbes.JS**

As with any AEM development, you can use any editor that is able to handle JavaScript code – either NetBeans or IntelliJ, or if you are testing / developing in real-time in a test environment just use CRXDE Lite.

The functionality of CRXDE Lite is very well covered in the Adobe documentation [here](https://docs.adobe.com/docs/en/crx/2-3/developing/development_tools/developing_with_crxde_lite.html).

(!) Keep in mind that only the **Author** mode of AEM is supported so far in Hobbes.JS

Hobbes.JS already supports a lot of out of the box browser interactions, but if you do need something custom done, below you will find a very good example of a well written function.

![Hobbes.JS code snippet](images/word-image-1.png "Hobbes.JS code snippet")

Documenting you code is key in every development project, remember that!

You will need to write locators and custom functions in external files for code readability purposes.

1. For locators CSS and jQuery locators we have: **locators.js**
2. For functions we have: **functions.js**

These two files are loadable by Hobbes code and should always be used.

**Test Reporting**

1. Here is a sample of a Jenkins JUNIT report:

![Hobbes.JS Jenkins Integration](images/word-image-2.png "Hobbes.JS Jenkins Integration")

1. Next up we have the real time running of Hobbes in action:

![](images/word-image-3.png)
