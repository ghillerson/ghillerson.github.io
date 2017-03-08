[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdAnalyze.html)

[]()Analyze Command
===================

The <span class="AppCommand">analyze</span> command collects statistics for a specific table, or for an entire schema.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Once statistics have been collected for a schema or table, they are automatically used by the query optimizer.

Syntax

``` FcnSyntax
ANALYZE TABLE [schemaName'.']table-Name

ANALYZE SCHEMA schema-Name
```

table-Name

The name of the table you want to analyze, which can optionally be qualified by its schema name. If you don't specify a <span class="ItalicFont">schemaName</span>, the current schema is assumed.

You must have insert permission for the table to be able to run this command.

schema-Name

The name of the schema you want to analyze.

You must have insert permission for all tables in the schema to be able to run this command.

[]()Analyze Table

The <span class="CodeFont">ANALYZE TABLE</span>command collects statistics for a specific table in the current schema. It also collects statistics for the index associated with the table in the schema. For example, if you have the following in your database:

-   a table named <span class="CodeFont">myTable</span>
-   <span class="CodeFont">myTable</span> has two indices: <span class="CodeFont">myTableIndex1</span> and <span class="CodeFont">myTableIndex2</span>

Then <span class="CodeFont">ANALYZE TABLE</span> will collect statistics for <span class="CodeFont">myTable</span>, <span class="CodeFont">myTableIndex1</span>, and <span class="CodeFont">myTableIndex2</span>.

The <span class="CodeFont">ANALYZE TABLE</span> command displays the following information for each index in the table:

| Value            | Description                                                                         |
|------------------|-------------------------------------------------------------------------------------|
| schemaName       | The name of the schema.                                                             |
| tableName        | The name of the table.                                                              |
| regionsCollected | The number of regions for which a collection was performed.                         |
| taskExecuted     | The number of collection tasks submitted. Note that this includes any failed tasks. |
| rowsCollected    | The total number of rows collected for the table.                                   |

[]()Analyze Schema

The <span class="CodeFont">ANALYZE SCHEMA</span> command collects statistics for every table in the schema. It also collects statistics for the index associated with every table in the schema. For example, if you have the following situation:

-   a schema named <span class="CodeFont">mySchema</span>
-   <span class="CodeFont">mySchema</span> contains two tables: <span class="CodeFont">myTable1</span> and <span class="CodeFont">myTable2</span>
-   <span class="CodeFont">myTable1</span> has two indices: <span class="CodeFont">myTable1Index1</span> and <span class="CodeFont">myTable1Index2</span>

Then the <span class="CodeFont">ANALYZE SCHEMA</span> command will collect statistics for <span class="CodeFont">myTable1</span>, <span class="CodeFont">myTable2</span>, <span class="CodeFont">myTable1Index1</span>, and <span class="CodeFont">myTable1Index2</span>.

The <span class="CodeFont">ANALYZE SCHEMA</span> command displays the following information for each table and for each index and its associated index in the schema:

| Value            | Description                                                                         |
|------------------|-------------------------------------------------------------------------------------|
| schemaName       | The name of the schema.                                                             |
| tableName        | The name of the table.                                                              |
| regionsCollected | The number of regions for which a collection was performed.                         |
| taskExecuted     | The number of collection tasks submitted. Note that this includes any failed tasks. |
| rowsCollected    | The total number of rows collected for the table.                                   |

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>This command operates like the <span class="CodeFont">[SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS](../SQLReference/BuiltInSysProcs/CollectSchemaStats.html)</span> built-in system procedure.

Examples

``` AppCommand
splice> analyze table myTable;
schemaName       |regionsCol&|tasksExecu&|rowsCollected|tableName
---------------------------------------------------------------------------
MYSCHEMA         |1          |1          |0            |MYTABLE1
MYSCHEMA         |1          |1          |0            |MYTABLE1_INDEX1
MYSCHEMA         |1          |1          |0            |MYTABLE1_INDEX2
3 rows selected

splice> analyze schema mySchema
schemaName       |regionsCol&|tasksExecu&|rowsCollected|tableName
---------------------------------------------------------------------------
MYSCHEMA         |1          |1          |0            |MYTABLE1
MYSCHEMA         |1          |1          |0            |MYTABLE1_INDEX1
MYSCHEMA         |1          |1          |0            |MYTABLE1_INDEX2
MYSCHEMA         |1          |1          |0            |MYTABLE2
MYSCHEMA         |1          |1          |0            |MYTABLE2_INDEX1
5 rows selected

splice>
```

 


