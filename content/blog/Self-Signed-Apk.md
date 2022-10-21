---
title: Signed apk to PlayStore
date: 2018-12-11 23:33:52
tags: ['javascript', 'coding', 'react native'] 
cover: 
    src: https://st1.bgr.in/wp-content/uploads/2018/02/android-p.jpg
---

Hi today i want to share how to signed android apps to play store(react native,cordova,etc)

your apk must be signed first..
signing your apk

Generate your keystore

```bash
keytool -genkey -v -dname 'CN=Alfathdirk,OU=YourAPK,O=GeekyAnts,L=Indonesia,ST=Jakarta,C=IN' -keystore yourkeystore.keystore -keypass yourpassword -storepass yourpassword -alias yourkeystore -keyalg RSA -keysize 2048 -validity 10000
```

Download certificate

download `deployment_cert.der` for your apps on `https://play.google.com/apps/publish/` menu App Signing

Validating and Zip your Apk

```bash
keytool -importcert -file deployment_cert.der -keystore yourkeystore.keystore
jarsigner -verbose -keystore yourkeystore.keystore app-release-unsigned.apk yourkeystore
zipalign -v -p 4  app-release-unsigned.apk my-app-unsigned-aligned.apk
apksigner sign --ks yourkeystore.keystore --out my-app-release.apk my-app-unsigned-aligned.apk
apksigner verify my-app-release.apk
```