[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysColPerms.html)

<a href="" id="SystemTables.SysColPerms"></a>[]()SYSCOLPERMS System Table
=========================================================================

The <span class="CodeFont">SYSCOLPERMS</span> table stores the column permissions that have been granted but not revoked.

All of the permissions for one (<span class="CodeFont">GRANTEE, TABLEID, TYPE, GRANTOR</span>) combination are specified in a single row in the <span class="CodeFont">SYSCOLPERMS</span> table. The keys for the <span class="CodeFont">SYSCOLPERMS</span> table are:

-   Primary key (<span class="CodeFont">GRANTEE, TABLEID, TYPE, GRANTOR</span>)
-   Unique key (<span class="CodeFont">COLPERMSID</span>)
-   Foreign key (<span class="CodeFont">TABLEID</span> references <span class="CodeFont">SYS.SYSTABLES</span>)

The following table shows the contents of the <span class="CodeFont">SYSCOLPERMS</span> system table.

| Column Name | Type                                                                                          | Length | Nullable | Contents                                                                                                                 |
|-------------|-----------------------------------------------------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------|
| COLPERMSID  | CHAR                                                                                          | 36     | NO       | Used by the dependency manager to track the dependency of a view, trigger, or constraint on the column level permissions |
| GRANTEE     | VARCHAR                                                                                       | 128    | NO       | The authorization ID of the user or role to which the privilege was granted                                              |
| GRANTOR     | VARCHAR                                                                                       | 128    | NO       | The authorization ID of the user who granted the privilege. Privileges can be granted only by the object owner           |
| TABLEID     | CHAR                                                                                          | 36     | NO       | The unique identifier for the table on which the permissions have been granted                                           |
| TYPE        | CHAR                                                                                          | 1      | NO       | If the privilege is non-grantable, the valid values are:                                                                 
                                                                                                                                   -   <span class="CodeFont">'s'</span> for <span class="CodeFont">SELECT</span>                                            
                                                                                                                                   -   <span class="CodeFont">'u'</span> for <span class="CodeFont">UPDATE</span>                                            
                                                                                                                                   -   <span class="CodeFont">'r'</span> for <span class="CodeFont">REFERENCES</span>                                        
                                                                                                                                                                                                                                                             
                                                                                                                                   If the privilege is grantable, the valid values are:                                                                      
                                                                                                                                                                                                                                                             
                                                                                                                                   -   <span class="CodeFont">'S'</span> for <span class="CodeFont">SELECT</span>                                            
                                                                                                                                   -   <span class="CodeFont">'U'</span> for <span class="CodeFont">UPDATE</span>                                            
                                                                                                                                   -   <span class="CodeFont">'R'</span> for <span class="CodeFont">REFERENCES</span>                                        |
| COLUMNS     | <span class="ItalicFont">org.apache.Splice Machine. iapi.services.io. FormatableBitSet</span> 
               This class is not part of the public API.                                                      | -1     | NO       | A list of columns to which the privilege applies                                                                         |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


