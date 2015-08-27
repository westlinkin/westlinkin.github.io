---
layout: post
title: Why I prefer AppCode over Xcode
tags: 
- iOS-development
- IDE
shortUrl: http://goo.gl/1YN82p
---

For the past four months, I've been learning iOS development. Basically I just read a [book](http://www.amazon.com/Beginning-iPhone-Development-Exploring-iOS-ebook/dp/B00M4FC7O6/ref=mt_kindle?_encoding=UTF8&me=), and then started writing code. I haven't started `Swift` language yet, for most iOS open-source libraries are written in `Objective-C`. And I think I won't start using `Swift` in another one or two years.

As an Android developer, I am used to `Android Studio`, which is a fantastic IDE for coding. For those Android developers who havn't using `Android Studio`yet, I strongly recommend you try it. 

When I started using `Xcode` for iOS development, I am very confused.

### What is wrong with Xcode

##### I accidentally close projects all the time.
`cmd + w` is a common shortcut for close a tab or window on OSX. If you're using `Safari` or `Chrome`, you know what I mean. If there are more than one tab in your brower when you use `cmd + w`, it close the focused tab. If there is no tab left, it close the window. It's quite easy to understand, right? But NOOOO, `Xcode` doesn't behave like that. If you use `cmd + w`, it close the whole project.

##### Delete a whole line? NO!
You can't use `cmd + delete` to delete a whole line, which is also a common shortcut on OSX. Yes, you can delete a whole line of code using `cmd + delete`, but if there is just an extra line and you wanna to delete it? `cmd + delete` will delete the line and delete half the line above it.

##### Code completion sucks
If you wanna use a certain method in a `NSObject`, which has a word `index` in it, but you can't remenber the whole name of the method, what will you do? Look up the document or source code to get the exact name or the first letter of the method? Because `Xcode` can only auto-complete code from the beginning. For example, if you type in `[Object index`, the IDE won't tell you all the methods related to `index` keyword, it can only tell you the methods started with `index`. This really makes writing code slower.

##### NO Auto-import
Why not? Even `Eclipse` has this feature a long long time ago. I can't stand that when I am writing a method/function, the IDE tells me:" Oh, I can't recognize this. Oh, you can't use that".

##### Can you really see the Log?
The font and line spacing of the Log console is a disaster. The text is bold and line spacing is way too small. So the log just looks like a black block. I can't really distinguish one log from another.

##### CocoaPods
`CocoaPods` is a dependency manager for iOS development, like `gradle` or `maven` for Android and Java. To use `CocoaPods` in your project, you can follow the steps on the [CocoaPods website](https://cocoapods.org/). This is not convenient enough! Becuase you need to use the terminal, which `Xcode` do not provide a shortcut to open and relocate to the project folder. You will have to open a terminal, then go to the project folder, or go to the project folder in finder and open a terminal there. Finally you need to run a command line to install the dependencies. Why all the trouble? `AppCode` can do all that for you, all you need to do is editing the `Podfile`.

### AppCode is better
`AppCode` fixes all the complaints I have about `Xcode`, plus I can use all the keymap I am already familiar with in `Android Studio`. Just export the keymap settings in `Android Studio` and import it in `AppCode`.

You can find out many other better feature of `AppCode` on the [official website](https://www.jetbrains.com/objc/features/). I am sure there are a lot to explore. You can find some tricks and tips on the [AppCode Blog](http://blog.jetbrains.com/objc/). This IDE truely makes my life a lot easier.

### Flaws in AppCode
`AppCode` is not perfect, though. When it comes to edit `xib` or `storyboard` file, it is crappy. And `AppCode` sure cannot submit apps to the AppStore. It's also not that good when editing the project settings.

Now my workflow of a new project is this: 

1. Create new project using `Xcode`
2. Config `CocoaPods` in `AppCode`
3. Edit `xib` and `storyboard` in `Xcode`
4. Write `Objective-C` code in `AppCode`
5. Config project in `Xcode`
6. Submit to beta test or AppStore in `Xcode`

Because `AppCode` can sync code and files instantly with `Xcode`, you don't need to worry about conflicts when editing the same project/file using two IDEs.

### Others
I don't mean starting an argument about which IDE is better. It's just, to me, `Xcode` is not good enough. I can be more efficient and focused when using `AppCode`, that's what really matters.

If you are always an `Xcode` user, you can try a [30-day trial](https://www.jetbrains.com/objc/download/) of `AppCode`, I mean, it doesn't hurt, does it? If you don't like, leave it there, delete it, do whatever you want with it. But if you like it, you will find out it really is an productivity tool. After all, IDE should make coder efficiency, right?

