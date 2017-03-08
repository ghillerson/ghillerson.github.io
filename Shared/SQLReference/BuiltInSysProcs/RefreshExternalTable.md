[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/RefreshExternalTable.html)

[]()SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE
===============================================

You call the SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE system procedure to manually refresh the schema of an external table in Splice Machine that has been modified outside of Spark. When you use the external table, Spark caches its schema in memory to improve performance; as long as you are using Spark to modify the table, it is smart enough to refresh the cached schema. However, if the table schema is modified outside of Spark, you need to call SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_REFRESH_EXTERNAL_TABLE( 
           String schemaName,
           String tableName )
```

schemaName

Specifies the schema of the table. Passing a <span class="CodeFont">null</span> or non-existent schema name generates an error.

table Name

The table name.

Results

This procedure does not return a result.

Example

This refreshes the schema of the external table named <span class="CodeFont">myTable</span>:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_REFRESH_EXTERNAL_TABLE('APP', 'myTable');
Statement executed.
```

See Also

-   [CREATE EXTERNAL TABLE](../Statements/CreateExternalTable.html)

 


