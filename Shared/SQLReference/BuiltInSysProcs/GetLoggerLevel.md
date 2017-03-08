[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetLoggerLevel.html)

<a href="" id="BuiltInSysProcs.GetLoggerLevel"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL
============================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL system procedure displays the logging level of the specified logger.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You can read more about Splice  Machine loggers and logging levels in the [Logging](../../Developers/TuningAndDebugging/UsingLogging.html) topic of our <span class="ItalicFont">Administrator's Guide</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_LOGGER_LEVEL(loggerName)
```

loggerName

A string specifying the name of the logger whose logging level you want to find.

You can find all of the available loggers by using the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_GET\_LOGGERS](GetLoggers.html)</span> system procedure.

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL</span> include these values:

|                                     |                                                                                                                                                                                                                               |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="BoldFont">Value</span> | <span class="BoldFont">Description</span>                                                                                                                                                                                     |
| LOGLEVEL                            | The level of the logger. This is one of the following values, which are described in the [Logging](../../Developers/TuningAndDebugging/UsingLogging.html) topic in our <span class="ItalicFont">Administrator's Guide</span>: 
                                                                                                                                                                                                                                                                      
                                       -   TRACE                                                                                                                                                                                                                      
                                       -   DEBUG                                                                                                                                                                                                                      
                                       -   INFO                                                                                                                                                                                                                       
                                       -   WARN                                                                                                                                                                                                                       
                                       -   ERROR                                                                                                                                                                                                                      
                                       -   FATAL                                                                                                                                                                                                                      |

Example

Here are two examples of using this procedure:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_LOGGER_LEVEL('com.splicemachine.utils.SpliceUtilities');
LOG&
----
WARN

1 row selected

splice> CALL SYSCS_UTIL.SYSCS_GET_LOGGER_LEVEL('com.splicemachine.mrio.api');
LOGL&
-----
DEBUG

1 row selected
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGERS</span>](GetLoggers.html)
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL</span>](SetLoggerLevel.html)
-   <span class="ItalicFont">[Splice Machine Logging](../../Developers/TuningAndDebugging/UsingLogging.html)</span> in our <span class="ItalicFont">Administrator's Guide</span>.

 


