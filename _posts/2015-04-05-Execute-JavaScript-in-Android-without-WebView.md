---
layout: post
title: Execute JavaScript in Android without WebView
tags: 
- Android
- JavaScript
- WebView
shortUrl: http://goo.gl/IkacIQ
---

For some reason, I need to execute JavaScript code in an Android project. Because the JavaScript code was running in a background thread(in `doInBackground` part in an [`AsyncTask`](http://developer.android.com/reference/android/os/AsyncTask.html)), I don't want to use `WebView`.

### Why not WebView

First of all, WebView is heavy. WebView is slow, especially in a large/huge project. Plus, you need to add a lot of WebView related settings to just execute one code snippet. It's just simply not worth it.

Secondly, WebView is UI related. A WebView should be created in UI thread. Sure, you can create it in UI thread, load JavaScript code in a background thread, then pass the result back to UI thread. It's workable, but it's not safe.

> If you call methods on WebView from any thread other than your app's UI thread, it can cause unexpected results. [[source](https://developer.android.com/guide/webapps/migrating.html#Threads)]

Last but not least, WebView is fragmented. After Android 4.4(API level 19), Android is using WebView baseed on [Chromuim](http://www.chromium.org/Home). Although this is toally a good thing, the WebView in Android 4.3 and below suffers the old version. You should code two version of WebView related code to just make it work. A lot of code should be re-write according to [this article](https://developer.android.com/guide/webapps/migrating.html).

Luckily, the good people in Mozilla make a project called `Rhino`. It is typically embedded into Java applications to provide scripting to end users.


### How to use Rhino

Rhino is a open source project, you can get the source code using this command:

```
git clone https://github.com/mozilla/rhino.git
```

Or fork their project on [GitHub](https://github.com/mozilla/rhino).

Of course, you don't have to get the source code. If you want to use it in your Android project. [Download Rhino](https://github.com/mozilla/rhino/releases/download/Rhino1_7R5_RELEASE/rhino1_7R5.zip) first, unzip it, put the `js.jar` file under `libs` folder. It is very small, so you don't need to worry your apk file will be ridiculously large because of this one external jar.

Here is some simple code to execute JavaScript code.

```java
Object[] params = new Object[] { "javaScriptParam" };

// Every Rhino VM begins with the enter()
// This Context is not Android's Context
Context rhino = Context.enter();

// Turn off optimization to make Rhino Android compatible
rhino.setOptimizationLevel(-1);
try {
    Scriptable scope = rhino.initStandardObjects();
    
    // Note the forth argument is 1, which means the JavaScript source has
    // been compressed to only one line using something like YUI
    rhino.evaluateString(scope, javaScriptCode, "JavaScript", 1, null);
    
    // Get the functionName defined in JavaScriptCode
    Object obj = scope.get(functionNameInJavaScriptCode, scope);
    
    if (obj instanceof Function) {
        Function jsFunction = (Function) obj;
        
        // Call the function with params
        Object jsResult = jsFunction.call(rhino, scope, scope, params);
        // Parse the jsResult object to a String
        String result = Context.toString(jsResult);
    }
} finally {
    Context.exit();
}

```

As you can see, it is quite easy. You can dig up more in [Rhino document](https://developer.mozilla.org/en-US/docs/Rhino_documentation).


### Proguard & Obfuscation

You can set up Rhino's proguard setting by adding this following line into your `proguard-android.txt` file.

```
-keep class org.mozilla.javascript.** { *; }
```

When you run the `assembleRelease` task, with `minifyEnabled true` of course, you still can see a lot of warning like these:

```
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class javax.swing.JMenu
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class javax.swing.JMenu
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class javax.swing.JMenu
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class javax.swing.ButtonGroup
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class javax.swing.JScrollPane
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class java.awt.event.ActionEvent
Warning: org.mozilla.javascript.tools.shell.JSConsole: can't find referenced class java.awt.event.ActionEvent
Warning: org.mozilla.javascript.tools.shell.JSConsole$1: can't find referenced class javax.swing.filechooser.FileFilter
Warning: org.mozilla.javascript.tools.shell.JSConsole$2: can't find referenced class java.awt.event.WindowAdapter
Warning: org.mozilla.javascript.tools.shell.JSConsole$2: can't find referenced class java.awt.event.WindowEvent
Warning: org.mozilla.javascript.tools.shell.JSConsole$2: can't find referenced class java.awt.event.WindowEvent
Warning: org.mozilla.javascript.xml.impl.xmlbeans.LogicalEquality: can't find referenced class org.apache.xmlbeans.XmlCursor
Warning: org.mozilla.javascript.xml.impl.xmlbeans.LogicalEquality: can't find referenced class org.apache.xmlbeans.XmlCursor
Warning: org.mozilla.javascript.xml.impl.xmlbeans.LogicalEquality: can't find referenced class org.apache.xmlbeans.XmlCursor
```

Luckily, evan with these warnings, the app runs fine. You can ignore them(that's what I do), or adding this line inot your `proguard-android.txt` file.

```
-dontwarn org.mozilla.javascript.**
```
