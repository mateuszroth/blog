---
title: 'Cordova overview & plugins'
tags:
  - Mobile
  - Cordova
  - Android
categories:
  - [Mobile, Cordova]
date: 2020-07-17 20:00:00
---
## Debugging
At that time, when I needed to find a bug on Android, I had to build the web app, build the Android app with Cordova, launch it on a device or an emulator, launch chrome dev tool to connect to the running app, put my breakpoints, find a possible cause, fix it in my code and do this process all over again. This whole process was taking way too much time.
```
$ cordova platform add <platform>
$ cordova platform remove <platform>
$ cordova requirements <platform>
```
## iOS emulators list
```
$ cordova emulate ios --list
```
## To emulate iOS 12+
```
$ cordova run ios --emulator --target="iPad-Air-2, 12.1" --buildFlag="-UseModernBuildSystem=0"
// -l --livereload doesn't work
```

## Run on a device
```
$ cordova run android --device
```

## Use emulator with VSCode and live reload (Ionic)
https://geeklearning.io/live-debug-your-cordova-ionic-application-with-visual-studio-code/

# iOS
https://developer.apple.com/download/more/ 
https://download.developer.apple.com/Developer_Tools/Xcode_9.4.1/Xcode_9.4.1.xip

# Android

## Cordova Android
https://cordova.apache.org/docs/en/latest/guide/platforms/android/#setting-environment-variables

## How to create AVD
https://developer.android.com/studio/run/managing-avds#viewing

## Android Emulator
https://developer.android.com/studio/run/emulator#about

## Start the emulator from the command line
https://developer.android.com/studio/run/emulator-commandline


# Threading

## Threading in Android Java:
http://burnignorance.com/phonegap-tips-and-tricks/implementing-multi-threading-in-android-plugin-for-phonegap-2-6-0/
```java
- (void) create
{
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        [self saySomething];
    });
}
```

## Cordova plugin Android threading
https://stackoverflow.com/a/28980819

## Threading Cordova plugin iOS
https://cordova.apache.org/docs/en/latest/guide/platforms/ios/plugin.html#threading

## iOS and Android difference
```
Plugin methods ordinarily execute in the same thread as the main interface. 
https://cordova.apache.org/docs/en/latest/guide/platforms/ios/plugin.html#threading
```
but on Android:
```
The plugin's JavaScript does not run in the main thread of the WebView interface; instead, it runs on the WebCore thread, as does the execute method.
https://cordova.apache.org/docs/en/latest/guide/platforms/android/plugin.html#threading
```