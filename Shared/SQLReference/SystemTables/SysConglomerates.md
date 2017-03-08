[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysConglomerates.html)

<a href="" id="SystemTables.SysConglomerates"></a>[]()SYSCONGLOMERATES System Table
===================================================================================

The <span class="CodeFont">SYSCONGLOMERATES</span> table describes the conglomerates within the current database. A conglomerate is a unit of storage and is either a table or an index.

The following table shows the contents of the <span class="CodeFont">SYSCONGLOMERATES</span> system table.

| Column Name        | Type                                                                             | Length | Nullable | Contents                                                                           |
|--------------------|----------------------------------------------------------------------------------|--------|----------|------------------------------------------------------------------------------------|
| SCHEMAID           | CHAR                                                                             | 36     | NO       | Schema ID for the conglomerate                                                     |
| TABLEID            | CHAR                                                                             | 36     | NO       | Identifier for table (join with SYSTABLES.TABLEID)                                 |
| CONGLOMERATENUMBER | BIGINT                                                                           | 19     | NO       | Conglomerate ID for the conglomerate (heap or index)                               |
| CONGLOMERATENAME   | VARCHAR                                                                          | 128    | YES      | Index name, if conglomerate is an index, otherwise the table ID                    |
| ISINDEX            | BOOLEAN                                                                          | 1      | NO       | Whether or not conglomerate is an index                                            |
| DESCRIPTOR         | <span class="ItalicFont">org.apache.splicemachine.catalog.IndexDescriptor</span> 
                      This class is not part of the public API.                                         | -1     | YES      | System type describing the index                                                   |
| ISCONSTRAINT       | BOOLEAN                                                                          | 1      | YES      | Whether or not the conglomerate is a system-generated index enforcing a constraint |
| CONGLOMERATEID     | CHAR                                                                             | 36     | NO       | Unique identifier for the conglomerate                                             |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


