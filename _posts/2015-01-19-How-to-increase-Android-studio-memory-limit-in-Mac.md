---
layout: post
title: How to increase Android Studio memory limit in Mac
tags: 
- Android
- AndroidStudio
shortUrl: http://goo.gl/PJc4hz
---

The [technical doc](http://tools.android.com/tech-docs/configuration) of configuring Android Studio on the Android Tools Project site is out dated. So you can not increase memory limit by configuring the `studio.vmoptions` file under `~/Library/Preferences/AndroidStudio/` folder. Actually, in my case, there is no `studio.vmoptions` or `idea.properties` file like the doc said.

### Locate the configuration file

If you are using `Terminal`, run command

```
open -e /Applications/Android\ Studio.app/Contents/bin/studio.vmoptions
```

Or, you can also open `Applications` folder in Finder, press `ctrl` then click or just right-click on Android Studio, choose `Show Package Contents`, you can find `studio.vmoptions` file under `Contents/bin` folder.

### Config your settings

You can just edit your `studio.vmoptions` file, increasing your `Xms` and `Xmx`.

`Xmx` specifies the maximum memory allocation pool for a Java Virtual Machine (JVM), while `Xms` specifies the initial memory allocation pool. Your JVM will be started with Xms amount of memory and will be able to use a maximum of Xmx amount of memory.

This is my configuration:

```
-Xms128m
-Xmx4096m
-XX:MaxPermSize=1024m
-XX:ReservedCodeCacheSize=200m
-XX:+UseCompressedOops
```

Once you make the changes, don't forget to **RESTART** Android Studio.

### Other

If you want to fall back to default values, here it is:

```
-Xms128m
-Xmx750m
-XX:MaxPermSize=350m
-XX:ReservedCodeCacheSize=96m
-XX:+UseCompressedOops
```

Or you can [download](http://tools.android.com/tech-docs/configuration) it from the Android Tools Project Site.

I think increasing the memory limit in IntelliJ IDEA is the same, I didn't check it though.


