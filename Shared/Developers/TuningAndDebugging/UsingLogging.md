[Open topic with navigation](../../../index.html#Shared/Developers/TuningAndDebugging/UsingLogging.html)

[]()Splice Machine Logging
==========================

This topic describes the logging facility used in Splice Machine. Splice Machine also allows you to exercise direct control over logging in your database. You can:

-   [Manually enable logging](#Manually) of all SQL statements.
-   Configure individual logger objects to log [specific message levels.](#Levels)
-   Call the <span class="CodeFont">log</span> function for a specific logger object, passing it a logging level value and a message. If the logger is currently configured to record messages at the specified level, the message is added to the log; otherwise, the logger ignores the message. Logger levels are ordered hierarchically; any message with a level equal to or greater than the hierarchical level for which logging is enabled is recorded into the log.

Splice Machine uses the open source [Apache log4j Logging API](http://logging.apache.org/log4j/1.2/manual.html), which allows you to associate a logger object with any java class, among other features. Loggers can be set to capture different levels of information.

Logging too much information can slow your system down, but not logging enough information makes it difficult to debug certain issues. The [Splice Machine Loggers](#SpliceLoggers) section below summarizes the loggers used by Splice Machine and the system components that they use. You can use the SQL logging functions described in the [SQL Logger Functions](#LoggerFunctions) section below to retrieve or modify the logging level of any logger used in Splice Machine.

[]()Manually Enabling Logging
-----------------------------

If you want to log all of your SQL statements, you can manually enable logging in these ways:

-   You can pass an argument to your Splice Machine JVM startup script, as follows:

    ``` Example
    -Dderby.language.logStatementText=true
    ```

-   You can add the following property definition to your <span class="CodeFont">hbase-default.xml</span>, <span class="CodeFont">hbase-site.xml</span>, or <span class="CodeFont">splice-site.xml</span> file:

    ``` Example
    <property>
    <name>splice.debug.logStatementContext</name>
    <value>true</value>
    <description>Property to enable logging of all statements.</description>
    </property>
    ```

You can examine the logged data in the the <span class="CodeFont">splice-derby.log</span> file, which is found in the <span class="CodeFont">splicemachine</span> directory.

### []()Logger Levels

The <span class="CodeFont">log4j</span> API defines six logger levels. The following table displays them from the lowest level to the highest:

| Logger Level | What gets logged for a logger object set to this level                                                                                                                                                                        |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TRACE        | Captures all messages.                                                                                                                                                                                                        |
| DEBUG        | Captures any message whose level is <span class="CodeFont">DEBUG</span>, <span class="CodeFont">INFO</span>, <span class="CodeFont">WARN</span>, <span class="CodeFont">ERROR</span>, or <span class="CodeFont">FATAL</span>. |
| INFO         | Captures any message whose level is <span class="CodeFont">INFO</span>, <span class="CodeFont">WARN</span>, <span class="CodeFont">ERROR</span>, or <span class="CodeFont">FATAL</span>.                                      |
| WARN         | Captures any message whose level is <span class="CodeFont">WARN</span>, <span class="CodeFont">ERROR</span>, or <span class="CodeFont">FATAL</span>.                                                                          |
| ERROR        | Captures any message whose level is <span class="CodeFont">ERROR</span> or <span class="CodeFont">FATAL</span>.                                                                                                               |
| FATAL        | Captures only messages whose level is <span class="CodeFont">FATAL</span>.                                                                                                                                                    |

### []()Splice Machine Loggers

The following table summarizes the loggers used in the Splice Machine environment that might interest you if you're trying to debug performance issues in your database:

| Logger Name                                            | Default Level | Description                                                                                                     |
|--------------------------------------------------------|---------------|-----------------------------------------------------------------------------------------------------------------|
| org.apache                                             | ERROR         | Logs all Apache software messages                                                                               |
| com.splicemachine.db                                   | WARN          | Logs all Derby software messages                                                                                |
| com.splicemachine.db.shared.common.sanity              | ERROR         | Logs all Derby Sanity Manager messages                                                                          |
| com.splicemachine.derby.impl.sql.catalog               | WARN          | Logs Derby SQL catalog/dictionary messages                                                                      |
| com.splicemachine.db.impl.sql.execute.operations       | WARN          | Logs Derby SQL operation messages                                                                               |
| org.apache.zookeeper.server.ZooKeeperServer            | INFO          | Used to determine when Zookeeper is started                                                                     |
| org.apache.zookeeper.server.persistence.FileTxnSnapLog | INFO          | Logs Zookeeper transactions                                                                                     |
| com.splicemachine                                      | WARN          | By default, controls all Splice Machine logging                                                                 |
| com.splicemachine.derby.hbase.SpliceDriver             | INFO          | Prints start-up and shutdown messages to the log and to the console                                             |
| com.splicemachine.derby.management.StatementManager    | ERROR         | Set the level of this logger to <span class="CodeFont">TRACE</span> to record execution time for SQL statements |

### []()SQL Logger Functions

Splice Machine SQL includes the following built-in system procedures, all documented in our [<span class="ItalicFont">SQL Reference Manual</span>](../../SQLReference/Intro.SQLReference.html), for interacting with the Splice Machine logs:

| System Procedure                                                                                | Description                                                 |
|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_GET\_LOGGERS](../../SQLReference/BuiltInSysProcs/GetLoggers.html)           | Displays a list of the active loggers.                      |
| [SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL](../../SQLReference/BuiltInSysProcs/GetLoggerLevel.html) | Displays the current logging level of the specified logger. |
| [SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL](../../SQLReference/BuiltInSysProcs/SetLoggerLevel.html) | Sets the current logging level of the specified logger.     |

See Also
--------

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGERS</span>](../../SQLReference/BuiltInSysProcs/GetLoggers.html) in the <span class="ItalicFont">SQL Reference Manual</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL</span>](../../SQLReference/BuiltInSysProcs/GetLoggerLevel.html) in the <span class="ItalicFont">SQL Reference Manual</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL</span>](../../SQLReference/BuiltInSysProcs/SetLoggerLevel.html) in the <span class="ItalicFont">SQL Reference Manual</span>

 


