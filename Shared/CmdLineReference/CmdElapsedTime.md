[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdElapsedTime.html)

[]()ElapsedTime Command
=======================

The <span class="AppCommand">elapsedtime</span> command is enables or disables having the command line interface display the amount of time required for a command to complete its execution.

Syntax

``` FcnSyntax
ELAPSEDTIME { ON | OFF }
```

ON

Enables display of the elapsed time by the command line interface. When this is enabled, you'll see how much time elapsed during execution of the command line.

OFF

Disables display of the elapsed time.

Examples

``` AppCommand
splice> elapsedtime on;
splice> VALUES current_date;
1
----------
2014-06-24
ELAPSED TIME = 2134 milliseconds
splice>
```

 


