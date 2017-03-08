[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/SetLoggerLevel.html)

<a href="" id="BuiltInSysProcs.SetLoggerLevel"></a>[]()SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL
============================================================================================

The SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL system procedure changes the logging level of the specified logger.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You can read more about Splice  Machine loggers and logging levels in the [Logging](../../Developers/TuningAndDebugging/UsingLogging.html) topic in our <span class="ItalicFont">Administrator's Guide</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_SET_LOGGER_LEVEL(loggerName, logLevel)
```

loggerName

A string specifying the name of the logger whose log level you want to find.

loggerLevel

A string specifying the new level to assign to the named logger. This must be one of the following level values, which are described in the [Logging](../../Developers/TuningAndDebugging/UsingLogging.html) topic in our <span class="ItalicFont">Administrator's Guide</span>:

-   'TRACE'
-   'DEBUG'
-   'INFO'
-   'WARN'
-   'ERROR'
-   'FATAL'

Results

This procedure does not return a result.

Usage Notes

You can use the <span class="CodeFont">TRACE</span> option of the Splice Machine <span class="CodeFont">StatementManager</span> log to record the execution time of each statement:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SET_LOGGER_LEVEL ( 'com.splicemachine.utils.SpliceUtilities', 'TRACE');
Statement executed
```

You can find all of the available loggers by using the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_GET\_LOGGERS](GetLoggers.html)</span> system procedure.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SET_LOGGER_LEVEL( 'com.splicemachine.mrio.api', 'DEBUG' );
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGERS</span>](GetLoggers.html)
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL</span>](#)
-   <span class="ItalicFont">[Splice Machine Logging](../../Developers/TuningAndDebugging/UsingLogging.html)</span> in our <span class="ItalicFont">Administrator's Guide</span>.

 


