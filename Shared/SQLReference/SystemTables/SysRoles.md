[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysRoles.html)

<a href="" id="SystemTables.SysRoles"></a>[]()SYSROLES System Table
===================================================================

The <span class="CodeFont">SYSROLES</span> table stores the roles in the database.

A row in the <span class="CodeFont">SYSROLES</span> table represents one of the following:

-   A role definition (the result of a [<span class="CodeFont">CREATE ROLE</span> statement](../Statements/CreateRole.html))
-   A role grant

The keys for the <span class="CodeFont">SYSROLES</span> table are:

-   Primary key (<span class="CodeFont">GRANTEE, ROLEID, GRANTOR</span>)
-   Unique key (<span class="CodeFont">UUID</span>)

The following table shows the contents of the <span class="CodeFont">SYSROLES</span> system table.

| Column Name     | Type    | Length | Nullable | Contents                                                                                                                                                                                                                                                                                                                              |
|-----------------|---------|--------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UUID            | CHAR    | 36     | NO       | A unique identifier for this role                                                                                                                                                                                                                                                                                                     |
| ROLEID          | VARCHAR | 128    | NO       | The role name, after conversion to case normal form                                                                                                                                                                                                                                                                                   |
| GRANTEE         | VARCHAR | 128    | NO       | If the row represents a role grant, this is the authorization identifier of a user or role to which this role is granted. If the row represents a role definition, this is the database owner's user name.                                                                                                                            |
| GRANTOR         | VARCHAR | 128    | NO       | This is the authorization identifier of the user that granted this role. If the row represents a role definition, this is the authorization identifier <span class="CodeFont">\_SYSTEM</span>. If the row represents a role grant, this is the database owner's user name (since only the database owner can create and grant roles). |
| WITHADMINOPTION | CHAR    | 1      | NO       | A role definition is modelled as a grant from <span class="CodeFont">\_SYSTEM</span> to the database owner, so if the row represents a role definition, the value is always <span class="CodeFont">'Y'</span>.                                                                                                                        
                                                                                                                                                                                                                                                                                                                                                                                        
                                                 This means that the creator (the database owner) is always allowed to grant the newly created role. Currently roles cannot be granted <span class="CodeFont">WITH ADMIN OPTION</span>, so if the row represents a role grant, the value is always <span class="CodeFont">'N'</span>.                                                   |
| ISDEF           | CHAR    | 1      | NO       | If the row represents a role definition, this value is <span class="CodeFont">'Y'</span>. If the row represents a role grant, the value is <span class="CodeFont">'N'</span>.                                                                                                                                                         |

See Also

-   [About System Tables](Intro.SystemTables.html)
-   [<span class="CodeFont">CURRENT\_ROLE</span>](../BuiltInFcns/CurrentRole.html) function
-   [<span class="CodeFont">CREATE\_ROLE</span>](../Statements/CreateRole.html) statement
-   [<span class="CodeFont">DROP\_ROLE</span>](../Statements/DropRole.html) statement
-   [<span class="CodeFont">GRANT</span>](../Statements/Grant.html) statement
-   [<span class="CodeFont">REVOKE</span>](../Statements/Revoke.html) statement
-   [<span class="CodeFont">SET ROLE</span>](../Statements/SetRole.html) statement

 


