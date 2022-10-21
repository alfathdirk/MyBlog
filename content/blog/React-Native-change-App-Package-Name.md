---
title: React Native change App/Package Name
date: 2018-12-12 00:07:01
tags: ['javascript', 'react native']
cover: 
    src: http://thetechmint.com/wp-content/uploads/2018/11/Webp.net-resizeimage-1.png

---

There are things one may need to change in the release build for Android. Things like App Name are a case here. Suppose you start developing by initialising to a generic App Name and at the time of release one need to change to the actual App Name.

Generate with correct names

Before we move forward and change things in the final version of the app. There is a way to fix this from the beginning. Generate a react native app with a proper package name with the command below.

```bash
react-native init MyAwesome -package "com.saumya.app"
```
But however if at all you have initialised the app as

```bash
react-native init RnApp
```
then the option remains to hack things in the end.
So read on.

Change App Name
Lets start with App Name. This is the name thats visible in users screen. To change this name, you have to change it in strings.xml.

Full path is `android/app/src/main/res/values/strings.xml`
and the entry is

```bash
<string name="app_name">My Android App</string>
```

Change Package name
This is shown in the Play Store and the details in About App of your Android device. This should say something like com.myapp or com.company.appname or something similar.

To change this, you have to edit four files.

```bash
- android/app/src/main/java/com/reactNativeSampleApp/MainActivity.java
- android/app/src/main/java/com/reactNativeSampleApp/MainApplication.java
- android/app/src/main/AndroidManifest.xml ( optional as per my experience )
- android/app/build.gradle
```

SOURCE: https://saumya.github.io/ray/articles/72/