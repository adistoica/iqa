---
title: "Selenium & Internet Explorer 11 (IEDriver): Exception in thread org openqa selenium UnsupportedCommandException: Error 404: Not Found"
date: "2018-03-23"
cover:
  image: "/images/blog/browsers.png"
summary: "How to fix IEdriver issues"
---

While testing one of my Internet Explorer setups within Browserstack (**Win10, IE11, Selenium 3.10** - all are being the latest production versions), I've noticed that after my tests just started I would randomly get:

```
 Exception in thread "Thread-4" org.openqa.selenium.UnsupportedCommandException: Error 404: Not Found
Not Found
Command duration or timeout: 32 milliseconds
\[...\]
Driver info: org.openqa.selenium.ie.InternetExplorerDriver
Capabilities \[{platform=WINDOWS, javascriptEnabled=true, elementScrollBehavior=0, ignoreZoomSetting=false, enablePersistentHover=true, ie.ensureCleanSession=false, browserName=internet explorer, enableElementCacheCleanup=true, unexpectedAlertBehaviour=dismiss, version=10, ie.usePerProcessProxy=false, cssSelectorsEnabled=true, ignoreProtectedModeSettings=true, requireWindowFocus=false, handlesAlerts=true, initialBrowserUrl=http://localhost:6461/, ie.forceCreateProcessApi=false, nativeEvents=true, browserAttachTimeout=0, ie.browserCommandLineSwitches=, takesScreenshot=true}\]
at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
\[...\]
```
Luckily after some googling for this issue, I've found out that IEDriver is not meant to be **ThreadSafe**. Moving forward, to fix this we would need a customer wrapper to extend the RemoteWebDriver class, so I came up with this:

```
package iqa.ro.selenium;

import org.openqa.selenium.Capabilities;
import org.openqa.selenium.remote.RemoteWebDriver;
import org.openqa.selenium.remote.Response;

import java.net.URL;
import java.util.Map;

/\*\*
 \* Synchronized variant of the RemoteWebDriver.
 \* Workaround for the IEDriver 404 error.
 \* @see: https://github.com/seleniumhq/selenium-google-code-issue-archive/issues/6592
 \*/
public class SynchronizedRemoteWebDriver extends RemoteWebDriver {

    private Object lock;

    /\* constructors \*/

    public SynchronizedRemoteWebDriver(URL remoteAddress, Capabilities capabilities) {
        super(remoteAddress, capabilities);
    }

    /\* overrides \*/

    @Override
    protected Response execute(String driverCommand, Map<String, ?> parameters) {
        synchronized (getLock()) {
            return super.execute(driverCommand, parameters);
        }
    }

    @Override
    protected Response execute(String command) {
        synchronized (getLock()) {
            return super.execute(command);
        }
    }

    /\* getters \*/

    public Object getLock() {
        if (lock == null) {
            // class level variable is not initialised if called from within constructor.
            lock = new Object();
        }
        return lock;
    }

}
```

Once you import the above class into your project, you just need to make use of it with something like this:

RemoteWebDriver = new SynchronizedRemoteWebDriver(new URL(url), convert(capabilities));
