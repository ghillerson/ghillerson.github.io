[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdSetConnection.html)

[]()Set Connection Command
==========================

The <span class="AppCommand">set connection</span> command allows you to specify which connection is the current connection, when you have more than one connection open.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If the specified connection does not exist, an error results, and the current connection is unchanged.

Syntax

``` FcnSyntax
SET CONNECTION Identifier
```

Identifier

The name of the connection that you want to be the current connection.

Examples

``` AppCommand
splice> connect 'jdbc:splice://abc:1527/splicedb;user=splice;password=admin' as sample1;
splice> connect 'jdbc:splice://xyz:1527/splicedb' as sample2;
splice (NEWDB)> show connections;
SAMPLE1 -    jdbc:splice://abc:1527/splicedb
SAMPLE2* -   jdbc:splice://xyz:1527/splicedb
* = current connection
splice(SAMPLE2)> set connection sample1;
splice(SAMPLE1)> disconnect all;
splice>
```

 


