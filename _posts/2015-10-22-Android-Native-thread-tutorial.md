---
layout: post
title: Using Android studio for NDK development
---
{% include JB/setup %}

In android, thread implementation is much simplifier using java, so why using the POSIX thread in native android?  
what is the pros and cons? According to the book <<Pro Android C with NDK>>, there are some reasons:
1. 






__Caution__  The JNIEnv interface pointer that is passed into each native method call is also valid in the
thread associated with the method call. It cannot be cached and used by other threads.
