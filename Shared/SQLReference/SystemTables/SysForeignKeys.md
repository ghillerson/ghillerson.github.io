[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysForeignKeys.html)

<a href="" id="SystemTables.SysForeignKeys"></a>[]()SYSFOREIGNKEYS System Table
===============================================================================

The <span class="CodeFont">SYSFOREIGNKEYS</span> table describes the information specific to foreign key constraints in the current database.

Splice Machine generates a backing index for each foreign key constraint. The name of this index is the same as <span class="CodeFont">SYSFOREIGNKEYS.CONGLOMERATEID</span>.

The following table shows the contents of the <span class="CodeFont">SYSFOREIGNKEYS</span> system table.

| Column Name     | Type | Length | Nullable | Contents                                                                                                                                                                                                   |
|-----------------|------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CONSTRAINTID    | CHAR | 36     | NO       | Unique identifier for the foreign key constraint (join with <span class="CodeFont">SYSCONSTRAINTS.CONSTRAINTID</span>)                                                                                     |
| CONGLOMERATEID  | CHAR | 36     | NO       | Unique identifier for index backing up the foreign key constraint (join with <span class="CodeFont">SYSCONGLOMERATES.CONGLOMERATEID</span>)                                                                |
| KEYCONSTRAINTID | CHAR | 36     | NO       | Unique identifier for the primary key or unique constraint referenced by this foreign key <span class="CodeFont">SYSKEYS.CONSTRAINTID</span> or <span class="CodeFont">SYSCONSTRAINTS.CONSTRAINTID</span>) |
| DELETERULE      | CHAR | 1      | NO       | Possible values:                                                                                                                                                                                           
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'R'</span> for <span class="CodeFont">NO ACTION</span> (default)                                                                                                                     
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'S'</span> for <span class="CodeFont">RESTRICT</span>                                                                                                                                
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'C'</span> for <span class="CodeFont">CASCADE</span>                                                                                                                                 
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'U'</span> for <span class="CodeFont">SET NULL</span>                                                                                                                                |
| UPDATERULE      | CHAR | 1      | NO       | Possible values:                                                                                                                                                                                           
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'R'</span> for <span class="CodeFont">NO ACTION</span> (default)                                                                                                                     
                                                                                                                                                                                                                                                          
                                              <span class="CodeFont">'S'</span> for <span class="CodeFont">RESTRICT</span>                                                                                                                                |

 


