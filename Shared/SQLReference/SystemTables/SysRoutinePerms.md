[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysRoutinePerms.html)

<a href="" id="SystemTables.SysRoutinePerms"></a>[]()SYSROUTINEPERMS System Table
=================================================================================

The <span class="CodeFont">SYSROUTINEPERMS</span> table stores the permissions that have been granted to routines.

Each routine <span class="CodeFont">EXECUTE</span> permission is specified in a row in the <span class="CodeFont">SYSROUTINEPERMS</span> table. The keys for the <span class="CodeFont">SYSROUTINEPERMS</span> table are:

-   Primary key (<span class="CodeFont">GRANTEE, ALIASID, GRANTOR</span>)
-   Unique key (<span class="CodeFont">ROUTINEPERMSID</span>)
-   Foreign key (<span class="CodeFont">ALIASID</span> references <span class="CodeFont">SYS.SYSALIASES</span>)

The following table shows the contents of the <span class="CodeFont">SYSROUTINEPERMS</span> system table.

| Column Name    | Type    | Length | Nullable | Contents                                                                                                                                                                                         |
|----------------|---------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ROUTINEPERMSID | CHAR    | 36     | NO       | Used by the dependency manager to track the dependency of a view, trigger, or constraint on the routine level permissions                                                                        |
| GRANTEE        | VARCHAR | 128    | NO       | The authorization ID of the user or role to which the privilege is granted                                                                                                                       |
| GRANTOR        | VARCHAR | 128    | NO       | The authorization ID of the user who granted the privilege. Privileges can be granted only by the object owner.                                                                                  |
| ALIASID        | CHAR    | 36     | NO       | The ID of the object of the required permission.                                                                                                                                                 
                                                                                                                                                                                                                                                  
                                                If <span class="CodeFont">PERMTYPE</span>=<span class="CodeFont">'E'</span>, the <span class="CodeFont">ALIASID</span> is a reference to the <span class="CodeFont">SYS.SYSALIASES</span> table.  
                                                                                                                                                                                                                                                  
                                                Otherwise, the <span class="CodeFont">ALIASID</span> is a reference to the <span class="CodeFont">SYS.SYSTABLES</span> table.                                                                     |
| GRANTOPTION    | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">GRANTEE</span> is the owner of the routine. Valid values are <span class="CodeFont">'Y'</span> and <span class="CodeFont">'N'</span>.                    |

 


