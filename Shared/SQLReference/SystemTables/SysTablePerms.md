[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysTablePerms.html)

<a href="" id="SystemTables.SysTablePerms"></a>[]()SYSTABLEPERMS System Table
=============================================================================

The <span class="CodeFont">SYSTABLEPERMS</span> table stores the table permissions that have been granted but not revoked.

All of the permissions for one (<span class="CodeFont">GRANTEE, TABLEID, GRANTOR</span>) combination are specified in a single row in the <span class="CodeFont">SYSTABLEPERMS</span> table. The keys for the <span class="CodeFont">SYSTABLEPERMS</span> table are:

-   Primary key (<span class="CodeFont">GRANTEE, TABLEID, GRANTOR</span>)
-   Unique key (<span class="CodeFont">TABLEPERMSID</span>)
-   Foreign key (<span class="CodeFont">TABLEID </span>references <span class="CodeFont">SYS.SYSTABLES</span>)

The following table shows the contents of the <span class="CodeFont">SYSTABLEPERMS</span> system table.

| Column Name    | Type    | Length | Nullable | Contents                                                                                                                |
|----------------|---------|--------|----------|-------------------------------------------------------------------------------------------------------------------------|
| TABLEPERMSID   | CHAR    | 36     | NO       | Used by the dependency manager to track the dependency of a view, trigger, or constraint on the table level permissions |
| GRANTEE        | VARCHAR | 128    | NO       | The authorization ID of the user or role to which the privilege is granted                                              |
| GRANTOR        | VARCHAR | 128    | NO       | The authorization ID of the user who granted the privilege. Privileges can be granted only by the object owner          |
| TABLEID        | CHAR    | 36     | NO       | The unique identifier for the table on which the permissions have been granted                                          |
| SELECTPRIV     | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">SELECT</span> permission is granted. The valid values are:                      
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |
| DELETEPRIV     | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">DELETE</span> permission is granted. The valid values are:                      
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |
| INSERTPRIV     | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">INSERT</span> permission is granted. The valid values are:                      
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |
| UPDATEPRIV     | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">UPDATE</span> permission is granted. The valid values are:                      
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |
| REFERENCESPRIV | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">REFERENCE</span> permission is granted. The valid values are:                   
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |
| TRIGGERPRIV    | CHAR    | 1      | NO       | Specifies if the <span class="CodeFont">TRIGGER</span> permission is granted. The valid values are:                     
                                                -   <span class="CodeFont">'y'</span> (non-grantable privilege)                                                          
                                                -   <span class="CodeFont">'Y'</span> (grantable privilege)                                                              
                                                -   <span class="CodeFont">'N'</span> (no privilege)                                                                     |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


