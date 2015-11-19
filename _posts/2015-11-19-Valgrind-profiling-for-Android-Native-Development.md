---
layout: default 
title: Valgrind for Android Native development
---

[Valgrind](http://valgrind.org/) is an instrumentation framework for building dynamic analysis tools. There are Valgrind tools that   
can automatically detect many memory management and threading bugs, and  profile your programs in detail. You can also use Valgrind  
to build new tools.

A quick guide of what valgrind could do: [memcheck functionality](http://www.thegeekstuff.com/2011/11/valgrind-memcheck/)!  

As now there is amount of developpers for NDK development in the filed which:  
<i>  
		1. Squeeze extra performance out of a device for computationally intensive applications like games or physics simulations.   
		2. Reuse your own or other developers' C or C++ libraries.  
</i>  

So the use of the valgrind for NDK developers is essential, this post could be used as a quick tour about valgrind installation and   
configuration, especially with the NDK toolchains.  

<h2>1. Valgrind installation</h2>  
The first thing is to download the latest version correspond to this blog, the version [valgrind-3.11.0](http://valgrind.org/downloads/valgrind-3.11.0.tar.bz2). Uzip it if a directory:  
 
		~/tool_tip/valgrind-3.11.0  

in my case.

	(1) cd ~/tool_tip/valgrind-3.11.0
  
	(2) Run ./configure, with some options if you wish.

	    The only interesting one is the usual --prefix=/where/you/want/it/installed.

	(3) Run "make".  

	(4) Run "make install", possibly as root if the destination permissions require that.  

	(5) See if it works.  Try "valgrind ls -l".

	(6) After step 5, in my case, the result shows:

		valgrind:  Fatal error at startup: a function redirection
		valgrind:  which is mandatory for this platform-tool combination
		valgrind:  cannot be set up.  Details of the redirection are:
		valgrind:  
		valgrind:  A must-be-redirected function
		valgrind:  whose name matches the pattern:      strlen
		valgrind:  in an object with soname matching:   ld-linux.so.2
		valgrind:  was not found whilst processing
		valgrind:  symbols from the object with soname: ld-linux.so.2
		valgrind:  
		valgrind:  Possible fixes: (1, short term): install glibc's debuginfo
		valgrind:  package on this machine.  (2, longer term): ask the packagers
		valgrind:  for your Linux distribution to please in future ship a non-
		valgrind:  stripped ld.so (or whatever the dynamic linker .so is called)
		valgrind:  that exports the above-named function using the standard
		valgrind:  calling conventions for this platform.  The package you need
		valgrind:  to install for fix (1) is called
		valgrind:  
		valgrind:    On Debian, Ubuntu:                 libc6-dbg
		valgrind:    On SuSE, openSuSE, Fedora, RHEL:   glibc-debuginfo
		valgrind:  
		valgrind:  Cannot continue -- exiting now.  Sorry.

	    which means Ubuntu is lack of libc6-dbg, a good way to install this package is:
			
			sudo aptitude install libc6-dbg  

<h2>2. Hello Valgrind !</h2>
So now you can using Valgrind to debug your program. The Valgrind tool suite provides a number of debugging and profiling tools that help you make your programs faster and more correct. The most popular of these tools is called Memcheck.

[My code](https://github.com/GiantGeorgeGo/keep-C/blob/master/valgrind_ndk/HelloVal.cpp) HelloVal.cpp:     

{% highlight c++ %}  
   
#include <stdio.h>
int main() {

	int *d;
	int e =*d;

	return 0;
}
{% endhighlight %}


compile it using g++ with -g or gcc -g with <i>-lstdc++</i>:
  
	gcc -lstdc++ -o HelloV HelloVal.cpp -g 

or simply:

	g++ -o HelloV HelloVal.cpp -g    

launch HelloV with valgrind:

		dir/to/your/installation/bin/valgrind --leak-check=yes HelloV  

			==3164== Memcheck, a memory error detector
			==3164== Copyright (C) 2002-2015, and GNU GPL'd, by Julian Seward et al.
			==3164== Using Valgrind-3.11.0 and LibVEX; rerun with -h for copyright info
			==3164== Command: /home/likewise-open/SPREADTRUM/george.yan/Nimes/keep-C/valgrind_ndk/HelloV
			==3164== 
			==3164== Use of uninitialised value of size 8
			==3164==    at 0x400606: main (HelloVal.cpp:9)
			==3164== 
			c=0.000 
			==3164== 
			==3164== HEAP SUMMARY:
			==3164==     in use at exit: 72,704 bytes in 1 blocks
			==3164==   total heap usage: 1 allocs, 0 frees, 72,704 bytes allocated
			==3164== 
			==3164== LEAK SUMMARY:
			==3164==    definitely lost: 0 bytes in 0 blocks
			==3164==    indirectly lost: 0 bytes in 0 blocks
			==3164==      possibly lost: 0 bytes in 0 blocks
			==3164==    still reachable: 72,704 bytes in 1 blocks
			==3164==         suppressed: 0 bytes in 0 blocks
			==3164== Rerun with --leak-check=full to see details of leaked memory
			==3164== 
			==3164== For counts of detected and suppressed errors, rerun with: -v
			==3164== Use --track-origins=yes to see where uninitialised values come from
			==3164== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 1 from 1)

			which says I have use of uninitialised value.

<h2>3. Valgrind configuration for android native development</h2>
I would highly recommend you to read valgrind's [README.android](http://valgrind.org/docs/manual/dist.readme-android.html), which give a detailed discussion of this.



<p>{{ page.date | date_to_string }}</p>
