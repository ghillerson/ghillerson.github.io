[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdRun.html)

[]()Run Command
===============

The <span class="AppCommand">run</span> command redirects the command line interpreter to read and process commands from the specified file. This continues until the end of the file is reached, or an [exit](CmdExit.html) command is executed. Note that the file <span class="ItalicFont">can</span> contain <span class="CodeFont">run</span> commands.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You can specify a file that is in the directory where you are running the command, or you can include the full file path so that the <span class="CodeFont">run</span> command can find it.

The command line interpreter prints out the statements in the file as it executes them.

Syntax

``` FcnSyntax
RUN String
```

String

The name of the file containing commands to execute.

Examples

``` AppCommand
splice> run 'setupMenuConn.spl';
splice> -- this is setupMenuConn.spl
-- splice displays its contents as it processes file
splice> connect 'jdbc:splice://xyz:1527/splicedb';
splice> autocommit off;
splice> -- this is the end of setupMenuConn.spl
-- there is now a connection to splicedb on xyz and no autocommit.
-- input will now resume from the previous source.
;
splice>
```

 


