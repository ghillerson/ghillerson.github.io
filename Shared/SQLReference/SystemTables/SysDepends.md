[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysDepends.html)

<a href="" id="SystemTables.SysDepends"></a>[]()SYSDEPENDS System Table
=======================================================================

The <span class="CodeFont">SYSDEPENDS</span> table stores the dependency relationships between persistent objects in the database.

Persistent objects can be dependents or providers. Dependents are objects that depend on other objects. Providers are objects that other objects depend on.

-   Dependents are views, constraints, or triggers.
-   Providers are tables, conglomerates, constraints, or privileges.

The following table shows the contents of the <span class="CodeFont">SYSDEPENDS</span> system table.

| Column Name     | Type                                                                        | Length | Nullable | Contents                                                                                             |
|-----------------|-----------------------------------------------------------------------------|--------|----------|------------------------------------------------------------------------------------------------------|
| DEPENDENTID     | CHAR                                                                        | 36     | NO       | A unique identifier for the dependent                                                                |
| DEPENDENTFINDER | <span class="ItalicFont">com.splicemachine.db.catalog.TypeDescriptor</span> 
                   This class is not part of the public API.                                    | -1     | NO       | A system type that describes the view, constraint, or trigger that is the dependent                  |
| PROVIDERID      | CHAR                                                                        | 36     | NO       | A unique identifier for the provider                                                                 |
| PROVIDERFINDER  | <span class="ItalicFont">com.splicemachine.db.catalog.TypeDescriptor</span> 
                                                                                                
                   This class is not part of the public API.                                    | -1     | NO       | A system type that describes the table, conglomerate, constraint, and privilege that is the provider |

 


