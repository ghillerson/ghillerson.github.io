[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysColumns.html)

<a href="" id="SystemTables.SysColumns"></a>[]()SYSCOLUMNS System Table
=======================================================================

The <span class="CodeFont">SYSCOLUMNS</span> table describes the columns within all tables in the current database.

The following table shows the contents of the <span class="CodeFont">SYSCOLUMNS</span> system table.

| Column Name        | Type                                                                        | Length | Nullable | Contents                                                                                                                                                                                                                                                                                                |
|--------------------|-----------------------------------------------------------------------------|--------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| REFERENCEID        | CHAR                                                                        | 36     | NO       | Identifier for table (join with <span class="CodeFont">SYSTABLES.TABLEID</span>)                                                                                                                                                                                                                        |
| COLUMNNAME         | VARCHAR                                                                     | 128    | NO       | Column or parameter name                                                                                                                                                                                                                                                                                |
| COLUMNNUMBER       | INTEGER                                                                     | 10     | NO       | The position of the column within the table                                                                                                                                                                                                                                                             |
| COLUMNDATATYPE     | <span class="ItalicFont">com.splicemachine.db.catalog.TypeDescriptor</span> 
                      This class is not part of the public API.                                    | -1     | NO       | System type that describes precision, length, scale, nullability, type name, and storage type of data. For a user-defined type, this column can hold a <span class="ItalicFont">TypeDescriptor</span> that refers to the appropriate type alias in <span class="CodeFont">SYS.SYSALIASES</span>.        |
| COLUMNDEFAULT      | <span class="ItalicFont">java.io.Serializable</span>                        | -1     | YES      | For tables, describes default value of the column. The <span class="ItalicFont">toString()</span> method on the object stored in the table returns the text of the default value as specified in the <span class="CodeFont">CREATE TABLE</span> or <span class="CodeFont">ALTER TABLE</span> statement. |
| COLUMNDEFAULTID    | CHAR                                                                        | 36     | YES      | Unique identifier for the default value                                                                                                                                                                                                                                                                 |
| AUTOINCREMENTVALUE | BIGINT                                                                      | 19     | YES      | What the next value for column will be, if the column is an identity column                                                                                                                                                                                                                             |
| AUTOINCREMENTSTART | BIGINT                                                                      | 19     | YES      | Initial value of column (if specified), if it is an identity column                                                                                                                                                                                                                                     |
| AUTOINCREMENTINC   | BIGINT                                                                      | 19     | YES      | Amount column value is automatically incremented (if specified), if the column is an identity column                                                                                                                                                                                                    |
| COLLECTSTATS       | BOOLEAN                                                                     | 1      | YES      | Whether or not to collect statistics on the table.                                                                                                                                                                                                                                                      |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


