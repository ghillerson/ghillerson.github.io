[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdDisconnect.html)

[]()Disconnect Command
======================

The <span class="AppCommand">disconnect</span> command disconnects from a database. It issues a <span class="CodeFont">java.sql.Connection.close</span> request for the current connection, or for the connection(s) specified on the command line.

Note that disconnecting from a database does not stop the command line interface or shut down Splice Machine. You can use the [exit](CmdExit.html) command to close out of the command line interface.

Syntax

``` FcnSyntax
DISCONNECT [ALL | CURRENT | connectionIdentifier]
```

ALL

All known connections are closed; as a result, there will not be a current connection.

CURRENT

The current connection is closed. This is the default behavior.

connectionIdentifier

The name of the connection to close; this must be same identifier assigned when the connection was opened with a [Connect](CmdConnect.html) command.

Examples

``` AppCommand
splice> connect 'jdbc:splice://xyz:1527/splicedb';
splice> -- we create a new table in splicedb: 
CREATE TABLE menu(course CHAR(10), ITEM char(20), PRICE integer);
0 rows inserted/updated/deleted
splice> disconnect;
splice>
```

 


