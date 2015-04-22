---
layout: post
title: Change Android studio Logcat text color to Eclipse style
tags: 
- Android
- JavaScript
- WebView
shortUrl: http://goo.gl/N44eHH
---

Android studio is better than Eclipse with ADT in almost every way. I've been using it for almost a year now. However, Logcat is an exception. Only `Assert`, `Error` and `Warn` log level's text has different color, which makes it very dificult to distinguish between `Info`, `Debug` and `Verbose` log level. And I believe these three log levels are mostly common used by app developers (including me of course).

### Locate Logcat Settings

Open Android Studio preferences (press `cmd + ,` if on OSX), you can find Android Logcat settings in 

```
Editor ==> Colors & Fonts ==> Android Logcat

```

Click `Save As...` button to save the current scheme, name it.

Uncheck the `Use inherited attributes` checkbox, in order to change the text style.

### Find Eclipse Logcat style

You can find the Eclipse Logcat color setting in the follow foottrace in preferences:

```
Android ==> LogCat ==> Colors
```

In case you have already deleted Eclipse or didn't bother to open it, here is the RGB color of each log levels:

```
Verbose:  000000
Debug: 00007F
Info: 027F00
Warn: FF7F00
Error: FF0000
Assert: FF0000
```

### Others
I use the Android studio default `Assert` color to make it different from `Error` log level.

I use the Android studio default theme, not `Darcular`, so the Eclipse logcat style works for me. If you are using the dark `Darcular` theme, there is already [a good color set](https://plus.google.com/+CyrilMottier/posts/Q6cZdf57cj7) for it.

Finnaly, here is the colorful logcat:
![img](/images/android-studio-logcat.png)

