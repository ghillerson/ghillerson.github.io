[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysPerms.html)

<a href="" id="SystemTables.SysPerms"></a>[]()SYSPERMS System Table
===================================================================

The <span class="CodeFont">SYSPERMS</span> table describes the <span class="CodeFont">USAGE</span> permissions for sequence generators and user-defined types.

The following table shows the contents of the <span class="CodeFont">SYSPERMS</span> system table.

| Column Name | Type    | Length | Nullable | Contents                                                                                                                                                                                                                             |
|-------------|---------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UUID        | CHAR    | 36     | NO       | The unique ID of the permission. This is the primary key.                                                                                                                                                                            |
| OBJECTTYPE  | VARCHAR | 36     | NO       | The kind of object receiving the permission. The only valid values are:                                                                                                                                                              
                                                                                                                                                                                                                                                                                   
                                             -   <span class="CodeFont">'SEQUENCE'</span>                                                                                                                                                                                          
                                             -   <span class="CodeFont">'TYPE'</span>                                                                                                                                                                                              |
| OBJECTID    | CHAR    | 36     | NO       | The <span class="CodeFont">UUID</span> of the object receiving the permission.                                                                                                                                                       
                                                                                                                                                                                                                                                                                   
                                             For sequence generators, the only valid values are <span class="CodeFont">SEQUENCEIDs</span> in the <span class="CodeFont">SYS.SYSSEQUENCES</span> table.                                                                             
                                                                                                                                                                                                                                                                                   
                                             For user-defined types, the only valid values are <span class="CodeFont">ALIASIDs</span> in the <span class="CodeFont">SYS.SYSALIASES</span> table if the <span class="CodeFont">SYSALIASES</span> ow describes a user-defined type.  |
| PERMISSION  | CHAR    | 36     | NO       | The type of the permission. The only valid value is <span class="CodeFont">'USAGE'</span>.                                                                                                                                           |
| GRANTOR     | VARCHAR | 128    | NO       | The authorization ID of the user who granted the privilege. Privileges can be granted only by the object owner.                                                                                                                      |
| GRANTEE     | VARCHAR | 128    | NO       | The authorization ID of the user or role to which the privilege was granted                                                                                                                                                          |
| ISGRANTABLE | CHAR    | 1      | NO       | If the <span class="CodeFont">GRANTEE</span> is the owner of the sequence generator or user-defined type, this value is <span class="CodeFont">'Y'</span>.                                                                           
                                                                                                                                                                                                                                                                                   
                                             If the <span class="CodeFont">GRANTEE</span> is not the owner of the sequence generator or user-defined type, this value is <span class="CodeFont">'N'</span>.                                                                        |

 


