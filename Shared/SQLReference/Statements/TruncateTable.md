[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/TruncateTable.html)

<a href="" id="Statements.TruncateTable"></a>[]()TRUNCATE TABLE
===============================================================

The <span class="CodeFont">TRUNCATE TABLE</span> statement allows you to quickly remove all content from the specified table and return it to its initial empty state.

To truncate a table, you must either be the database owner or the table owner.

You cannot truncate system tables or global temporary tables with this statement.

Syntax

``` FcnSyntax
TRUNCATE TABLE table-Name
```

table-Name

The name of the table to truncate.

Examples

To truncate the entire Players\_Test table, use the following statement:

``` Example
splice> TRUNCATE TABLE Players_Test;
0 rows inserted/updated/deleted
```

 


