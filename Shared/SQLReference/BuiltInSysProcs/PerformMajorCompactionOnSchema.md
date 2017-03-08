[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/PerformMajorCompactionOnSchema.html)

<a href="" id="BuiltInSysProcs.PerformMajorCompactionOnSchema"></a>[]()SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_SCHEMA
================================================================================================================================

The SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_SCHEMA system procedure performs a major compaction on a schema. The compaction is performed on all of the tables in the schema, and on all of its index and constraint tables for each table in the schema.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_PERFORM_MAJOR_COMPACTION_ON_SCHEMA(schemaName)
```

schemaName

A string that specifies the Splice Machine schema name to which the table belongs.

Usage

Major compaction is synchronous, which means that when you invoke this procedure from the command line, your command line prompt won't be available again until the compaction completes, which can take a little time.

Results

This procedure does not return a result.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_PERFORM_MAJOR_COMPACTION_ON_SCHEMA('SPLICE');
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE</span>](EmptyStatementCache.html)

 


