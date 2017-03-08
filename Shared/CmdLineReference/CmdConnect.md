[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdConnect.html)

[]()Connect Command
===================

The <span class="AppCommand">connect</span> command connects to the database specified by <span class="CodeFont">ConnectionURLString</span>. It connects by issuing a <span class="CodeFont">getConnection</span> request with the specified URL, using <span class="CodeFont">java.sql.DriverManager </span>or <span class="CodeFont">javax.sql.DataSource </span>to set the current connection to that URL.

Syntax

``` FcnSyntax
CONNECT ConnectionURLString
   [ AS Identifier ]
```

ConnectionURLString

The URL of the database.

Identifier

The optional name that you want to assign to the connection.

If the connection succeeds, the connection becomes the current one and all further commands are processed against the new, current connection.

Example 1: Connecting on a Cluster

If you are running Splice Machine on a cluster, connect from a machine that is NOT running an HBase RegionServer and specify the IP address of a <span class="HighlightedCode">regionServer</span> node, e.g. <span class="AppCommand">10.1.1.110</span>.

``` AppCommand
splice> connect 'jdbc:splice://regionServer:1527/splicedb';
```

Here are two specific examples, one of which includes a user ID and password in the connect string:

``` AppCommand
splice> connect 'jdbc:splice://10.1.1.110:1527/splicedb';

splice> connect 'jdbc:splice://10.1.1.110:1527/splicedb;user=splice;password=admin';
```

Example 2: Connecting to the Standalone Version

If you're using the standalone version of Splice Machine, specify <span class="HighlightedCode">localhost</span> instead.

``` AppCommand
splice> connect 'jdbc:splice://localhost:1527/splicedb';
```

Here is an example that includes a user ID and password in the connect string:

``` AppCommand
splice> connect 'jdbc:splice://localhost:1527/splicedb;user=joey;password=bossman';
```

 


