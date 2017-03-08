[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/RenameIndex.html)

<a href="" id="RefSection.RenameIndex"></a>[]()RENAME INDEX
===========================================================

The <span class="CodeFont">RENAME INDEX</span> statement allows you to rename an index in the current schema. Users cannot rename indexes in the <span class="CodeFont">SYS</span> schema.

Syntax

``` FcnSyntax
RENAME INDEX index-Name TO new-index-Name
```

index-Name

The name of the index to be renamed.

new-Index-Name

The new name for the index.

Example

``` Example
splice> RENAME INDEX myIdx TO Player_index;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">ALTER</span>](AlterTable.html) statement

 


