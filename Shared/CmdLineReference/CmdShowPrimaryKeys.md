[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowPrimaryKeys.html)

[]()Show PrimaryKeys
====================

The <span class="AppCommand">show primarykeys</span> command displays all the primary keys in the specified table.

Syntax

``` FcnSyntax
SHOW PRIMARYKEYS FROM schemaName.tableName
```

schemaName

The schema name.

tableName

The table name.

Results

The <span class="AppCommand">show primary keys</span> command results contains the following columns:

| Column Name  | Description                                    |
|--------------|------------------------------------------------|
| TABLE\_NAME  | The name of the table                          |
| COLUMN\_NAME | The name of the column                         |
| KEY\_SEQ     | The order of the column within the primary key |
| PK\_NAME     | The unique name of the constraint              |

Examples

``` AppCommand
splice> create table myTable(i int, j int, primary key (i,j));
0 rows inserted/updated/deleted

splice> show primarykeys from mySchema.myTable;
TABLE_NAME  |COLUMN_NAME  |KEY_SEQ  |PK_NAME
-------------------------------------------------------
A           |I            |1        |SQL141120202723310
A           |J            |2        |SQL141120202723310

2 rows selected
```

 


