[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysAliases.html)

<a href="" id="SystemTables.SysAliases"></a> []()SYSALIASES System Table
========================================================================

The <span class="CodeFont">SYSALIASES</span> table describes the procedures, functions, and user-defined types in the database.

The following table shows the contents of the <span class="CodeFont">SYSALIASES</span> system table.

| Column Name   | Type                                                                         | Length        | Nullable | Contents                                                                                                                                                 |
|---------------|------------------------------------------------------------------------------|---------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ALIASID       | CHAR                                                                         | 36            | NO       | Unique identifier for the alias                                                                                                                          |
| ALIAS         | VARCHAR                                                                      | 128           | NO       | Alias (in the case of a user-defined type, the name of the user-defined type)                                                                            |
| SCHEMAID      | CHAR                                                                         | 36            | YES      | Reserved for future use                                                                                                                                  |
| JAVACLASSNAME | LONG VARCHAR                                                                 | 2,147,483,647 | NO       | The Java class name                                                                                                                                      |
| ALIASTYPE     | CHAR                                                                         | 1             | NO       | <span class="ItalicFont">'F'</span> (function), <span class="ItalicFont">'P'</span> (procedure), <span class="ItalicFont">'A'</span> (user-defined type) |
| NAMESPACE     | CHAR                                                                         | 1             | NO       | <span class="ItalicFont">'F'</span> (function), <span class="ItalicFont">'P'</span> (procedure), <span class="ItalicFont">'A'</span> (user-defined type) |
| SYSTEMALIAS   | BOOLEAN                                                                      | 1             | NO       | <span class="ItalicFont">YES</span> (system supplied or built-in alias)                                                                                  
                                                                                                                           <span class="ItalicFont">NO</span> (alias created by a user)                                                                                              |
| ALIASINFO     | <span class="ItalicFont">org.apache.Splice Machine. catalog.AliasInfo</span> 
                 This class is not part of the public API.                                     | -1            | YES      | A Java interface that encapsulates the additional information that is specific to an alias                                                               |
| SPECIFICNAME  | VARCHAR                                                                      | 128           | NO       | System-generated identifier                                                                                                                              |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


