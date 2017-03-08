[Open topic with navigation](../../index.html#Shared/CmdLineReference/RLWrapSummary.html)

[]()rlWrap Commands Synopsis
============================

The <span class="CodeItalicFont">rlWrap</span> program is a <span class="ItalicFont">readline wrapper</span>, a small utility that uses the GNU <span class="CodeItalicFont">readline</span> library to allow the editing of keyboard input for any command; it also provides a history mechanism that is very handy for fixing or reusing commands. Splice Machine strongly recommends that you use <span class="CodeItalicFont">rlWrap</span> when interacting with your database via our command line interface, which is also known as the <span class="AppCommand">splice&gt;</span> prompt.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You can customize many aspects of <span class="CodeItalicFont">rlWrap</span> and <span class="CodeItalicFont">readline</span>, including the keyboard bindings for the available commands. For more information, see the Unix man page for <span class="CodeItalicFont">readline</span>.

The following table summarizes some of the common keyboard options you can use with <span class="CodeItalicFont">rlWrap</span>; this table uses the default bindings that are in place when you install <span class="CodeItalicFont">rlWrap</span> on MacOS; keyboard bindings may be different in your environment.

Command
Description
CTRL-@
Set mark
CTRL-A
Move to the beginning of the line
CTRL-B
Move back one character
CTRL-D
Delete the highlighted character
CTRL-E
Move to the end of the line
CTRL-F
Move forward one character
CTRL-H
Backward delete character
CTRL-J
Accept (submit) the line
CTRL-L
Clear the screen
CTRL-M
Accept the line
CTRL-N
Move to the next line in history
CTRL-P
Move to the previous line in history
CTRL-R
Reverse search through your command line history
CTRL-S
Forward search through your command line history
CTRL-T
Transpose characters: switch the highlighted character with the one preceding it
CTRL-U
Discard from the cursor position to the beginning of the line
CTRL-\]
Search for a character on the line
CTRL-\_
Undo
 
ALT-&lt;
Go to the beginning of the history
ALT-&gt;
Go to the end of the history
ALT-B
Backward word
ALT-C
Capitalize the current word
ALT-F
Forward word
ALT-L
Downcase word
ALT-R
Revert line
ALT-T
Transpose words
ALT-U
Uppercase word
Note that the <span class="AppCommand">ALT</span> key is labeled as the <span class="AppCommand">option</span> key on Macintosh keyboards.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you're using the <span class="CodeFont">splice&gt;</span> prompt in the Terminal.app on MacOS, the <span class="CodeFont">ALT-</span> commands listed above only work if you select the <span class="CodeFont">Use Option as Meta key</span> setting in the keyboard preferences for your terminal window

 


