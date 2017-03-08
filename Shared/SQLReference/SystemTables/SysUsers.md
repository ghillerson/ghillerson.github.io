[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysUsers.html)

<a href="" id="SystemTables.SysUsers"></a>[]()SYSUSERS System Table
===================================================================

The <span class="CodeFont">SYSUSERS</span> table stores user credentials when <span class="CodeFont">NATIVE</span> authentication is enabled.

When SQL authorization is enabled (as it is, for instance, when <span class="CodeFont">NATIVE</span> authentication is on) only the database owner can <span class="CodeFont">SELECT</span> from this table, and no one, not even the database owner, can <span class="CodeFont">SELECT</span> the <span class="CodeFont">PASSWORD</span> column.

The following table shows the contents of the <span class="CodeFont">SYSUSERS</span> system table.

| Column Name   | Type      | Length | Nullable | Contents                                                                     |
|---------------|-----------|--------|----------|------------------------------------------------------------------------------|
| USERNAME      | VARCHAR   | 128    | NO       | The user's name, the value of the user attribute on a connection URL.        |
| HASHINGSCHEME | VARCHAR   | 32672  | NO       | Describes how the password is hashed.                                        |
| PASSWORD      | VARCHAR   | 32672  | NO       | The password after applying the <span class="CodeFont">HASHINGSCHEME</span>. |
| LASTMODIFIED  | TIMESTAMP | 29     | NO       | The time when the password was last updated.                                 |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


