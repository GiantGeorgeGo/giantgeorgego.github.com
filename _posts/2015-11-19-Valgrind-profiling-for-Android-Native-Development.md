---
layout: post 
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
  




<p>{{ page.date | date_to_string }}</p>