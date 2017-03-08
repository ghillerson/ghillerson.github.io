[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/PerformMajorCompactionOnTable.html)

<a href="" id="BuiltInSysProcs.PerformMajorCompactionOnTable"></a>[]()SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE
==============================================================================================================================

The SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE system procedure performs a major compaction on a table. The compaction is performed on the table and on all of its index and constraint tables.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_PERFORM_MAJOR_COMPACTION_ON_TABLE(
                schemaName, tableName)
```

schemaName

A string that specifies the Splice Machine schema name to which the table belongs.

tableName

A string that specifies name of the Splice Machine table on which to perform the compaction.

Usage

Major compaction is synchronous, which means that when you invoke this procedure from the command line, your command line prompt won't be available again until the compaction completes, which can take a little time.

Results

This procedure does not return a result.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_PERFORM_MAJOR_COMPACTION_ON_TABLE('SPLICE','Pitching');
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_SCHEMA</span>](PerformMajorCompactionOnSchema.html)

 


