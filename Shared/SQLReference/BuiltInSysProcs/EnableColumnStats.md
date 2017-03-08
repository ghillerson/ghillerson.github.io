[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/EnableColumnStats.html)

SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS
======================================

The <span class="CodeFont">SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS</span> system procedure enables collection of statistics on a specific table column in your database.

Syntax

``` FcnSyntax
SYSCS_UTIL.ENABLE_COLUMN_STATISTICS(
                       VARCHAR(128) schema,
                       VARCHAR(128) table,
                       VARCHAR(128) columnName)
```

schemaName

Specifies the schema of the table. Passing a <span class="CodeFont">null</span> or non-existent schema name generates an error.

tableName

Specifies the table name of the table. The string must exactly match the case of the table name, and the argument of <span class="CodeFont">"Fred"</span> will be passed to SQL as the delimited identifier <span class="CodeFont">'Fred'</span>. Passing a <span class="CodeFont">null</span> or non-existent table name generates an error.

columnName

Specifies the name of the column for which you want statistics enabled. Passing a <span class="CodeFont">null</span> or non-existent column name generates an error.

Results

This procedure does not return a result.

Usage Notes

Here are some <span class="Highlighted">important notes</span> about collecting column statistics:

-   Statistics can only be collected on columns with data types that can be ordered; numeric types, some <span class="CodeFont">CHAR</span> types, some <span class="CodeFont">BIT</span> types, and date/time types can be ordered.

    You can determine if a data type can be ordered by examining the Comparisons table in the [Data Assignments and Comparisons](../DataTypes/DataTypeCompatability.html) topic: any data type with a <span class="CodeBoldFont">Y</span> in any column in that table can be ordered, and thus can have statistics collected on it.

-   Statistics are automatically collected on all columns by default.

SQL Examples

``` Example
splice> CALL SYSCS_UTIL.ENABLE_COLUMN_STATISTICS('SPLICE', 'Salaries', 'Salary');
Statement executed.
```

See Also

-   [Data Assignments and Comparisons](../DataTypes/DataTypeCompatability.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS</span>](DisableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS</span>](CollectSchemaStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS</span>](DropSchemaStats.html)
-   [Using Statistics](../../Developers/TuningAndDebugging/UsingStatistics.html) in the <span class="ItalicFont">Administrator's Guide</span>

 


