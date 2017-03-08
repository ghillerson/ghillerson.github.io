[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysStatements.html)

<a href="" id="SystemTables.SysStatements"></a>[]()SYSSTATEMENTS System Table
=============================================================================

The <span class="CodeFont">SYSSTATEMENTS</span> table describes the prepared statements in the database.

The table contains one row per stored prepared statement.

The following table shows the contents of the <span class="CodeFont">SYSSTATEMENTS</span> system table.

| Column Name         | Type         | Length | Nullable | Contents                                                                                                                                                                  |
|---------------------|--------------|--------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| STMTID              | CHAR         | 36     | NO       | Unique identifier for the statement                                                                                                                                       |
| STMTNAME            | VARCHAR      | 128    | NO       | Name of the statement                                                                                                                                                     |
| SCHEMAID            | CHAR         | 36     | NO       | The schema in which the statement resides                                                                                                                                 |
| TYPE                | CHAR         | 1      | NO       | Always <span class="CodeFont">'S'</span>                                                                                                                                  |
| VALID               | BOOLEAN      | 1      | NO       | Whether or not the statement is valid                                                                                                                                     |
| TEXT                | LONG VARCHAR | 32,700 | NO       | Text of the statement                                                                                                                                                     |
| LASTCOMPILED        | TIMESTAMP    | 29     | YES      | Time that the statement was compiled                                                                                                                                      |
| COMPILATIONSCHEMAID | CHAR         | 36     | NO       | ID of the schema containing the statement                                                                                                                                 |
| USINGTEXT           | LONG VARCHAR | 32,700 | YES      | Text of the <span class="CodeFont">USING</span> clause of the <span class="CodeFont">CREATE STATEMENT</span> and <span class="CodeFont">ALTER STATEMENT</span> statements |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


