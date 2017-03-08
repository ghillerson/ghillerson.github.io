[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowIndexes.html)

[]()Show Indexes
================

The <span class="AppCommand">show indexes</span> command displays all of the indexes in the database, the indexes in the specified schema, or the indexes on the specified table.

Syntax

``` FcnSyntax
SHOW INDEXES [ IN schemaName | FROM tableName ]
```

schemaName

If you supply a schema name, only the indexes in that schema are displayed.

tableName

If you supply a table name, only the indexes on that table are displayed.

Results

The <span class="AppCommand">show indexes</span> command results contains the following columns:

| Column Name  | Description                                                                |
|--------------|----------------------------------------------------------------------------|
| TABLE\_NAME  | The name of the table.                                                     |
| INDEX\_NAME  | The name of the index.                                                     |
| COLUMN\_NAME | The name of the column.                                                    |
| ORDINAL      | The position of the column in the index.                                   |
| NON\_UNIQUE  | Whether this is a unique or non-unique index.                              |
| TYPE         | The index type                                                             |
| ASC\_        | Indicates if this is an ascending (A) or descending (D) index.             |
| CONGLOM\_NO  | The conglomerate number, which points to the corresponding table in HBase. |

Examples

``` AppCommand
splice> show indexes in my_table;
TABLE_NAME    |INDEX_NAME       |COLUMN_NAME   |ORDINAL&|NON_UNIQUE|TYPE |ASC&|CONGLOM_NO
-----------------------------------------------------------------------------------------
MY_TABLE      |I1               |ID            |1       |true      |BTREE|A   |1937
MY_TABLE      |I1               |STATE_CD      |2       |true      |BTREE|A   |1937
MY_TABLE      |I1               |CITY          |3       |true      |BTREE|A   |1937
MY_TABLE      |I2               |ID            |1       |true      |BTREE|D   |1953
MY_TABLE      |I2               |STATE_CD      |2       |true      |BTREE|D   |1953
MY_TABLE      |I2               |CITY          |3       |true      |BTREE|D   |1953
MY_TABLE      |I3               |ID            |1       |true      |BTREE|D   |1969
MY_TABLE      |I3               |STATE_CD      |2       |true      |BTREE|A   |1969
MY_TABLE      |I3               |CITY          |3       |true      |BTREE|D   |1969
MY_TABLE      |I4               |LATITUDE      |1       |true      |BTREE|D   |1985
MY_TABLE      |I4               |STATE_CD      |2       |true      |BTREE|A   |1985
MY_TABLE      |I4               |ID            |3       |true      |BTREE|A   |1985
MY_TABLE      |I5               |ID            |1       |true      |BTREE|A   |2001
MY_TABLE      |I5               |ID            |2       |true      |BTREE|D   |2001

14 rows selected
splice>
```

 


