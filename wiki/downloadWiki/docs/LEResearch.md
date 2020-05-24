I did take some comparison between Locale Emulator(LE for short) with Ntleas, and the result LE was do better than Ntleas under Windows 7/8 even I fixed some compatible questions in NTLEA. This topic will dive a lil deep and may not very interesting :D
----
# Differences between Locale Emualtor & NTLEA
I use a game which is dependent on engine QLiE for example. see the main differences: 

: **Normal, note the center light grey text!**
: ![](LEResearch_https://www.codeplex.com/Download?ProjectName=ntlea&DownloadId=783605)
: **Locale Emulator, very well**
: ![](LEResearch_https://www.codeplex.com/Download?ProjectName=ntlea&DownloadId=783606)
: **NTLEA, oops ...**
: ![](LEResearch_https://www.codeplex.com/Download?ProjectName=ntlea&DownloadId=783607)

Those RadioButtons, ComboBoxes are messed up, these just the VCL's TRadioButton and TComboBox class, and those common controls won't enter into DefWindowProc with uMsg being {"WM_CREATE/WM_NCCREATE"}, which in NTLEA should do MultibytesToWideCharInternal, those steps missing would cause MultibyteString being Force converted to Unicode!

In fact, not only VCL but many controls will do the same. In NTLEA, there are code hooking on function "CallWindowProcA", the hooking method will put known control's windowproc, such as BUTTON, EDIT from ansi version to unicode version through "SendUnicodeMessage" function, there will do translation from MultiBytes toWideChars on many messages as "TopLevelWindowProc" function do. While VCL is not such 'fixed' & 'well-known', and even query class wndproc field by GetClassInfoA or GetClassInfoW, the return value is 0 (means no such info), and bad luck, you have only Ansi version wndproc!

I think the LE is done the trick more into syslevel, through a tech named 'SSDT Shadow Hook'(Shadow System Service Descriptor Table), by hooking functions like NtUserCallMessage, it can got those message and do what it should do.
# Ntleas' Approach
Ntleas could do like that, but LE have done and success, there is not necessarily to copy it, and maybe this action will bring antivirus warning and even more ... killing. and ntleas may lose the feature embedded into spoon (which is the main motivation to rewrite), I'd like to keep it only in UserLevel( if possible, support dual mode, but not now ;) ). 
----
Well a nice news here :D, the problem could be handled without do as LE did.

After 2 days dug into the trouble, I found these engine games were based on VCL(Borland Delphi), and those grabled strings were  all VCL common controls. They were do paint( on handled WM_PAINT message), when handling them WM_GETTEXT or WM_GETTEXTLENGTH, there alwasy inside the block WM_PAINT! All string could show normally if not being done with Unicode -> Ansi conversion! 
: ![](LEResearch_https://www.codeplex.com/Download?ProjectName=ntlea&DownloadId=784864)

Now, block it inside debugger, and see the callstack, OK, GetWindowTextW, but one thing still strange, why Get Unicode String Proc finally call Ansi Version of CallWindowProc??
: ![](LEResearch_https://www.codeplex.com/Download?ProjectName=ntlea&DownloadId=784865)

With a wrong direction, I took some tricks on reference count for avoid those "non convert cases", but totally failed. Finally the Author _AVC_ told me about new choice for taking care about SetWindowLongW, for that this might be used by VCL components, and I did with success. 

I don't know if this solved more garble-case others met. But, at least, the QLiE engine games could be shown as it should be Now, Happy :D!