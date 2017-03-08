[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysViews.html)

<a href="" id="SystemTables.SysViews"></a>[]()SYSVIEWS System Table
===================================================================

The <span class="CodeFont">SYSVIEWS</span> table describes the view definitions within the current database.

The following table shows the contents of the <span class="CodeFont">SYSVIEWS</span> system table.

| Column Name         | Type         | Length | Nullable | Contents                                                                                   |
|---------------------|--------------|--------|----------|--------------------------------------------------------------------------------------------|
| TABLEID             | CHAR         | 36     | NO       | Unique identifier for the view (join with <span class="CodeFont">SYSTABLES.TABLEID</span>) |
| VIEWDEFINITION      | LONG VARCHAR | 32,700 | NO       | Text of view definition                                                                    |
| CHECKOPTION         | CHAR         | 1      | NO       | <span class="CodeFont">'N'</span> (check option not supported yet)                         |
| COMPILATIONSCHEMAID | CHAR         | 36     | NO       | ID of the schema containing the view                                                       |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


