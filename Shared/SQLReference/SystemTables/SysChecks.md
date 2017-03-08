[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysChecks.html)

<a href="" id="SystemTables.SysChecks"></a>[]()SYSCHECKS System Table
=====================================================================

The <span class="CodeFont">SYSCHECKS</span> table describes the check constraints within the current database.

The following table shows the contents of the <span class="CodeFont">SYSCHECKS</span> system table.

| Column Name       | Type                                                                             | Length | Nullable | Contents                                                      |
|-------------------|----------------------------------------------------------------------------------|--------|----------|---------------------------------------------------------------|
| CONSTRAINTID      | CHAR                                                                             | 36     | NO       | Unique identifier for the constraint                          |
| CHECKDEFINITION   | LONG VARCHAR                                                                     | 32,700 | NO       | Text of check constraint definition                           |
| REFERENCEDCOLUMNS | <span class="ItalicFont">com.splicemachine. db.catalog. ReferencedColumns</span> 
                     This class is not part of the public API.                                         | -1     | NO       | Description of the columns referenced by the check constraint |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


