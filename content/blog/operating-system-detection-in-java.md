---
title: "Operating System Detection in Java"
date: "2017-07-16"
cover:
  image: "/images/blog/OS.jpeg"
summary: "How to do a basic OS detection in Java"
---


Here is the code snipped of the day: if you want to do a basic Operating System detection in Java (for some specific Selenium routines, let's say), you can use a simple class like the one below.

```
public final class OSDetection {

    public static String OS = null;

    public static String getOsName() {
        if (OS == null) {
            OS = System.getProperty("os.name");
        }
        return OS;
    }

    public static boolean isWindows() {
        return getOsName().startsWith("Windows");
    }

    public static boolean isUnix()
    {
        return getOsName().startsWith("Unix");
    }

    public static boolean isMac() {
        return getOsName().startsWith("Mac");
    }

}
```
###### After including the class above in your package, you could do something like:

```
if (OSDetection.isMac()) {
// you specific MacOS stuff here..
}

if (OSDetectionisUnix()) {
// you specific Unix/Linux stuff here..
}

if (OSDetectionisWindows()) {
// you specific Windows stuff here..
}
```

Have fun!
