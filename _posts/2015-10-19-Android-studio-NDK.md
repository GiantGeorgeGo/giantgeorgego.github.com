---
layout: post 
title: Using Android studio for NDK development
---
{% include JB/setup %}

<h2>{{ page.title }}</h2>
<i>A quick tutorial to NDK development using new version of Android Studio 1.4</i>

1. New a simple android application project in the AS and build the project. This will generate the class target objects for the java class. The generated objs will be located in:  
     
     app/build/intermediates/classes/debug.  

2. Creat a jni directory in app/src/main/, so you will get:  

```    
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
```
3. Make an declaration of the native method in the java code (main activity for example):  


     native String StringFromJni();  

4. Generate the JNI header file for the native method declared in step 3.  
   * launch a terminal, go to the class obj directory: __ProjectName__/app/build/intermediates/classes/debug  
   * use javah command to generate the c/c++ header files  
       
       $JDKPath$\bin\javah -jni -d $ModuleFileDir$/src/main/jni $FileClass$

       <i>Note:</i>  
       __JDKPath__ - refers to your JDK installation directory.  
       -jni - means generate JNI-style header file (default).  
       -d - output directory, point to your jni directory just crated in step 2.  
       __FileClass__ - com.example.georgeyan.nimes.Avignon. (the package name)

5. Now you can find the generated header file in your jni ditrctory (app/src/main/jni). The file name is __com_package_name_projectname_module__.h, containing:  


     JNIEXPORT jstring JNICALL Java_com_example_georgeyan_nimes_Avignon_StringFromJni(JNIEnv *, jobject);  

6. Now create a c/c++ source file to implement it.  

     JNIEXPORT jstring JNICALL Java_com_example_georgeyan_nimes_Avignon_StringFromJni(JNIEnv * env, jobject ){  
  
                       return (env)->NewStringUTF("HelloFromJni");
     }  

   Two ways to compile the .so module:  
   ** gradle: if you want more about gradle, refer to this:[gradle](http://gradle.org/).    
             add the following in the file app/build.gradle, in the __defaultConfig__ bracket:  

                     ndk {  
                          moduleName "hello-jni"  
                     }  

             add:    
	     
	     android.useDeprecatedNdk=true
	     
	     in the __gradle.properties__ if you encounter the build problem.  

   ** Android.mk: build manually, not pratice using Android Studio.  

7. The last thing is using the .so module in the java class.  

            ```
	    static {  
                     System.loadLibrary("hello-jni");  
            }  
	    ```

   Example:  
   In the Oncreate function:  
           ```  
           TextView text = (TextView)findViewById(R.id.hw);  
           
           text.setText(StringFromJni());  
	   ```  

8. Demo on github:  
           [Nimes](https://github.com/GiantGeorgeGo/Nimes.git).  


<p>{{ page.date | date_to_string }}</p>
