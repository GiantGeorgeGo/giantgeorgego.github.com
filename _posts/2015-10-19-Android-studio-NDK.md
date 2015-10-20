---
layout: post 
title: Using Android studio for NDK development
tagline: "Supporting tagline"
---
{% include JB/setup %}

<h2>{{ page.title }}</h2>
<i>A quick tutorial to NDK development using new version of Android Studio 1.4</i>

1. New a simple android application project in the AS and build the project. This will generate the class target objects for the java class. The generated objs will be located in:  
     
     app/build/intermediates/classes/debug.  

2. Creat a jni directory in app/src/main/, so you will get:  

    src  
    ├── androidTest  
    │   └── java  
    │   │   └── com  
    │   │   │   └── example  
    │   │   │   │   └── **project_name**  
    │   │   │   │   │   └── **module_name**  
    ├── main  
    │   ├── java  
    │   │   └── com  
    │   │   │        └── example  
    │   │   │   │           └── **project_name**  
    │   │   │   │   │               └── **module_name**  
    │   ├── **jni**  
    │   └── res  
    │   │       ├── drawable  
    │   │      ├── layout  
    │   │       ├── menu  
     ...  

3. Make an declaration of the native method in the java code (main activity for example):  

     native String StringFromJni();  

4. Generate the JNI header file for the native method declared in step 3.  
   * launch a terminal, go to the class obj directory: __ProjectName__/app/build/intermediates/classes/debug  
   * use javah command to generate the c/c++ header files  
       
       $JDKPath$\bin\javah -jni -d $ModuleFileDir$/src/main/jni $FileClass$

       <i>Note:</i>  
       ** JDKPath - refers to your JDK installation directory.  
       ** -jni - means generate JNI-style header file (default).  
       ** -d - output directory, point to your jni directory just crated in step 2.  
       ** FileClass - com.example.projectname.modulename. (the package name)

<p>{{ page.date | date_to_string }}</p>
