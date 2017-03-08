[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysTables.html)

<a href="" id="SystemTables.SysTables"></a>[]()SYSTABLES System Table
=====================================================================

The <span class="CodeFont">SYSTABLES</span> table describes the tables and views within the current database.

The following table shows the contents of the <span class="CodeFont">SYSTABLES</span> system table.

| Column Name     | Type    | Length | Nullable | Contents                                                               |
|-----------------|---------|--------|----------|------------------------------------------------------------------------|
| TABLEID         | CHAR    | 36     | NO       | Unique identifier for table or view                                    |
| TABLENAME       | VARCHAR | 128    | NO       | Table or view name                                                     |
| TABLETYPE       | CHAR    | 1      | NO       | Possible values are:                                                   
                                                                                                                         
                                                 -   <span class="CodeFont">'S'</span> (system table)                    
                                                 -   <span class="CodeFont">'T'</span> (user table)                      
                                                 -   <span class="CodeFont">'A'</span> (synonym)                         
                                                 -   <span class="CodeFont">'V'</span> (view)                            |
| SCHEMAID        | CHAR    | 36     | NO       | Schema ID for the table or view                                        |
| LOCKGRANULARITY | CHAR    | 1      | NO       | Lock granularity for the table:                                        
                                                                                                                         
                                                 -   <span class="CodeFont">'T'</span> (table level locking)             
                                                 -   <span class="CodeFont">'R'</span> (row level locking, the default)  |
| VERSION         | VARCHAR | 128    | YES      | Version ID.                                                            |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


