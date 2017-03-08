[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysConstraints.html)

<a href="" id="SystemTables.SysConstraints"></a>[]()SYSCONSTRAINTS System Table
===============================================================================

The <span class="CodeFont">SYSCONSTRAINTS</span> table describes the information common to all types of constraints within the current database (currently, this includes primary key, unique, and check constraints).

The following table shows the contents of the <span class="CodeFont">SYSCONSTRAINTS</span> system table.

| Column Name    | Type    | Length | Nullable | Contents                                                                                                                                                                                                                       |
|----------------|---------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CONSTRAINTID   | CHAR    | 36     | NO       | Unique identifier for constraint                                                                                                                                                                                               |
| TABLEID        | CHAR    | 36     | NO       | Identifier for table (join with <span class="CodeFont">SYSTABLES.TABLEID</span>)                                                                                                                                               |
| CONSTRAINTNAME | VARCHAR | 128    | NO       | Constraint name (internally generated if not specified by user)                                                                                                                                                                |
| TYPE           | CHAR    | 1      | NO       | Possible values:                                                                                                                                                                                                               
                                                                                                                                                                                                                                                                                
                                                -   <span class="CodeFont">'P'</span> for primary key)                                                                                                                                                                          
                                                -   <span class="CodeFont">'U'</span> for unique)                                                                                                                                                                               
                                                -   <span class="CodeFont">'C'</span> for check)                                                                                                                                                                                |
| SCHEMAID       | CHAR    | 36     | NO       | Identifier for schema that the constraint belongs to (join with <span class="CodeFont">SYSSCHEMAS.SCHEMAID</span>)                                                                                                             |
| STATE          | CHAR    | 1      | NO       | Possible values:                                                                                                                                                                                                               
                                                                                                                                                                                                                                                                                
                                                -   <span class="CodeFont">'E'</span> for enabled                                                                                                                                                                               
                                                -   <span class="CodeFont">'D'</span> for disabled                                                                                                                                                                              |
| REFERENCECOUNT | INTEGER | 10     | NO       | The count of the number of foreign key constraints that reference this constraint; this number can be greater than zero only or <span class="CodeFont">PRIMARY KEY</span> and <span class="CodeFont">UNIQUE</span> constraints |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


