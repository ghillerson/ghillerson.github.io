[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysKeys.html)

<a href="" id="SystemTables.SysKeys"></a>[]()SYSKEYS System Table
=================================================================

The <span class="CodeFont">SYSKEYS</span> table describes the specific information for primary key and unique constraints within the current database.

Splice Machine generates an index on the table to back up each such constraint. The index name is the same as <span class="CodeFont">SYSKEYS.CONGLOMERATEID</span>.

The following table shows the contents of the <span class="CodeFont">SYSKEYS</span> system table.

| Column Name    | Type | Length | Nullable | Contents                            |
|----------------|------|--------|----------|-------------------------------------|
| CONSTRAINTID   | CHAR | 36     | NO       | Unique identifier for constraint    |
| CONGLOMERATEID | CHAR | 36     | NO       | Unique identifier for backing index |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


