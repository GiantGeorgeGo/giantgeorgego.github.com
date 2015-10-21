---
layout: post
title: Debug native code using Android Studio
---
{% include JB/setup %}

<i>introduction of NDK debug</i>

The Android Studio 1.4 has already well equiped with the ndk debugger.

* Android studio debug setup
  
  1. Invoke "Run"->"Debug Configuration"->"Android Native".    
  2. Press **+** to add a Native Android Configuration.  
    
* Gradle configuration file, add the following lines in the app/build.gradle:  

      buildTypes {  
        release {  
            minifyEnabled false  
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'  
  
        }  
        debug {  
            debuggable = true  
            jniDebuggable = true  
        }  
    }  

* Invoke "Run"->"Debug app-native".  

