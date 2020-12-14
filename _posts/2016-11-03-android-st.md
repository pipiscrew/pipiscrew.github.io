---
title: android studio - build apk release with proguard
author: PipisCrew
date: 2016-11-03
categories: [android]
toc: true
---

write your rules at :
proguard-rules.pro

at build.gradle (module:app), fix the buildtypes tag :
```js
    buildTypes {
        release {
            debuggable false
            minifyEnabled true
            shrinkResources true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
           // signingConfig signingConfigs.config (used for preconfigured signing)
        }
        debug {
            //signingConfig signingConfigs.config (used for preconfigured signing)
        }
    }
```

my APK from 2.7mb went 1.8mb

references :
http://stackoverflow.com/a/35145658
https://gist.github.com/maheshwarLigade/7143ae567fe8ac7c1e20

origin - http://www.pipiscrew.com/?p=6243 android-studio-build-apk-release-with-proguard