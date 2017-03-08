[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowConnections.html)

[]()Show Connections
====================

The <span class="AppCommand">show connections</span> command displays a list of connection names and the URLs used to connect to them. The name of the current connection is marked with a trailing asterisk (<span class="CodeFont">\*</span>).

Syntax

``` FcnSyntax
SHOW CONNECTIONS
```

Examples

``` AppCommand
splice> connect 'jdbc:splice://abc:1527/splicedb' as sample1;
splice> connect 'jdbc:splice://xyz:1527/splicedb' as sample2;
splice (NEWDB)> show connections;
SAMPLE1 -    jdbc:splice://abc:1527/splicedb
SAMPLE2* -   jdbc:splice://xyz:1527/splicedb
* = current connection
splice(NEWDB)>
```

 


