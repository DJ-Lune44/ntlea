# **History Background and Inspiration to Ntleas**
Ntlea is another location emulator program written by _LoveHina Advance_ (_AVC_ in short) and _magami_(NtleaGUI), like Microsoft's Applocale, mainly for running applications without requiring user to switch Locale explicitly, in early 2008.

While the author _AVC_ is busy working, and ntlea core stopped maintaining support Windows 8 and 8.1, and sadly, ntlea will be no longer taking effect any more.

Ntlea uses Win32 API Low Level Hooking, and it is developped using Assembly code, the loader is coding using MASM, and the core Hook DLL is using GoASM Assembler. These 2 prevent many people who wanna do continue work on Ntlea.

Though there are some other choices instead, like [Locale Switch](http://kdays.cn/days/read.php?tid=182), [Locale Emulator](http://i.watashi.me/archives/locale-emulator.html)([src](https___github.com_xupefei_Locale-Emulator)), or even MS apploc, ntlea had its own features : 
# Small Executable size, fully opensource, simple hook method, direct source code(though asm);
# The only 1 known which is Compatible with Portable softwares(Maybe none kernel hooking system);
# Still lots of users knowing it and/or currently using it;
# support from Windows XP, which would be supported by M$ until 2015.7.14;
and: 
* If ntlea could running on windows 8/8.1, that must be wonderful!
* If ntlea could change fully or mostly using C source code, many developers may contribute on it more easily, being truely OpenSource Program!
After about 2 months work and test in my spare time on studying Ntlea hook tech between ASM and MSVC, I found it is possible to rewrite Ntlea with C source code(or say, only less than 1% code is Assembly)

considering that Win2000 and WinXP-SP1 were no longer most people to use, ntleas dropped those supports (actually, all code was there and had been translated to C, but haven't test them), transcode on XP-SP2/XP-SP3 will be continue supported, though whole XP will be discontinue supported by Microsoft.

Above all are the main inspirations/goals of rewriting ntlea to ntleas, with author's helping and my friends tests, and new one ntlea ... 
Finally Ntleas is now here !!
