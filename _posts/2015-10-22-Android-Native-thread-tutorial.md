---
layout: post
title: Using Android studio for NDK development
---
{% include JB/setup %}

In android, thread implementation is much simplifier using java, so why using the POSIX thread in native android?  
what is the pros and cons? According to the book <<Pro Android C with NDK>>, there are some reasons as listed:  

1. Assumes that the logic to assign tasks to threads is part of the Java code, since
there is no API in native space to create Java threads.  

<i>My understand is that if it is the native code who wants to invoke a new thread for a task, the native code have to cross the jni boundry to invoke the java code, this is a expensive cost.</i>  

2. Assumes that the native code is thread-safe, since Java-based threading is
transparent to the native code.  

3. Native code cannot benefit from other concurrent programming concepts and
components, such as semaphores, since no APIs for Java threads are available
in native space.  

4. Native code running in separate threads cannot communicate or share
resources directly  
  

 






__Caution__  The JNIEnv interface pointer that is passed into each native method call is also valid in the
thread associated with the method call. It cannot be cached and used by other threads.
