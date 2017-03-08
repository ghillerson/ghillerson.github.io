[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysSchemas.html)

<a href="" id="SystemTables.SysSchemas"></a>[]()SYSSCHEMAS System Table
=======================================================================

The <span class="CodeFont">SYSSCHEMAS</span> table describes the schemas within the current database.

The following table shows the contents of the <span class="CodeFont">SYSSCHEMAS</span> system table.

| Column Name     | Type    | Length | Nullable | Contents                                                |
|-----------------|---------|--------|----------|---------------------------------------------------------|
| SCHEMAID        | CHAR    | 36     | NO       | Unique identifier for the schema                        |
| SCHEMANAME      | VARCHAR | 128    | NO       | Schema name                                             |
| AUTHORIZATIONID | VARCHAR | 128    | NO       | The authorization identifier of the owner of the schema |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


