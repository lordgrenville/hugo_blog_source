+++
title = "Editing an Android App"
author = ["Josh Friedlander"]
date = 2022-06-01
draft = false
+++

Problem: I have an app I like. I want to make a trivial change to the text in one screen. Emailed the developer, he said I could just edit the file in the `assets` folder and sideload it (although he failed to see the point of the edit...)

Background: an APK is just a zipped archive, you can unzip it and edit the text files, then zip, rename to a `.apk` extension and try install it (easiest is `adb install /path/to/app.apk`). Since an Android app is compiled, most of the decompressed files will be binaries, but not all - some simple things are in plain text, including the ones I wanted to change.

Solved? Not quite. For security reasons, Android requires the app to be _signed_, so once I edited it and sent it back, it was lacking a signature and I got the error `Failure [INSTALL_PARSE_FAILED_NO_CERTIFICATES]`. OK, how do I sign it? The [Android Studio docs](https://developer.android.com/studio/publish/app-signing) have detailed instructions. I downloaded Android Studio, and hit a wall - the menu option `Build > Generate Signed Bundle/APK` just didn't exist on the menu. I looked at some online advice, but none of it helped. Anyway, I just wanted to generate a key pair, do I really need an entire IDE for that? Apparently not, the IDE is using a tool that comes with Java called `jarsigner` but I wasn't able to find this in my `%JAVA\_HOME%` and also hit permission issues (I was using WSL on Windows which may have been part of the cause).

Anyway, I eventually found a "batteries included" [repo](https://github.com/techexpertize/SignApk) claiming to do this for me. The signing worked, but the install still didn't. Maybe this was because the repo was eight years old? I found [a newer one](https://github.com/patrickfav/uber-apk-signer) which happily signed my APK, but installation still failed, with the error `[INSTALL_PARSE_FAILED_UNEXPECTED_EXCEPTION: Failed to parse /data/app...AndroidManifest.xml]`. What was wrong the AndroidManifest.xml? I hadn't touched it, and I couldn't read it because it was compiled. ([Here](https://blogs.sap.com/2014/05/21/how-to-modify-an-apk-file/) is a blog post from 2014, a more innocent time, which does what I did until here and succeeds.)

Time for the big guns. I downloaded [Apktool](https://ibotpeaches.github.io/Apktool/), a reverse-engineering tool that tries to restore the source. I was warned that this can break complicated apps, but the one I was editing is pretty simple and survived the compilation. Starting with my original `apk` file, I ran `apktool d myapp.apk`, edited the file in the assets, had a quick look at the now-readable `AndroidManifest.xml` (utterly ordinary, nothing of interest to see!), rebuilt the app with `apktool b myapp.zip.out -o edited_app.apk`, and then tried to install. No good - no certificate! Signed the new `apk` with `uber-apk-signer` and tried again: this time it was rejected with a new error: `[INSTALL_FAILED_UPDATE_INCOMPATIBLE]`. Looks like the problem is the old version existing on my phone. I uninstalled it, reran `adb install` and hey presto - it worked!

If this sounds like a tedious and horrible exercise to you, you're
probably right. But somehow my brain is wired to find the lure of the
solution greater than the frustration of the journey.

Summary:

-   Merely unzipping and editing doesn't work. Use `apktool` to reverse-engineer and a modern signing tool to generate a new signature
-   Uninstall the old version, and then `adb install`. (You'll lose your old settings, this way, so be ready to restore them.)
-   If you want to distribute your app to other people via the Play Store, you're beyond the scope of this post!
