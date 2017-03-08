[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/RenameTable.html)

<a href="" id="Statements.RenameTable"></a>[]()RENAME TABLE
===========================================================

The <span class="CodeFont">RENAME TABLE</span> statement allows you to rename an existing table in any schema (except the schema <span class="CodeFont">SYS</span>).

To rename a table, you must either be the database owner or the table owner.

Syntax

``` FcnSyntax
RENAME TABLE table-Name TO new-Table-Name
```

table-Name

The name of the table to be renamed.

new-Table-Name

The new name for the table.

Usage Notes

Attempting to rename a table generates an error if:

-   there is a view or a foreign key that references the table
-   there are any check constraints <span>or triggers </span>on the table

Example

``` Example
splice> RENAME TABLE MorePlayers to PlayersTest;
0 rows inserted/updated/deleted
```

See the [<span class="CodeFont">ALTER TABLE</span> statement](AlterTable.html) for more information.

See Also

-   [<span class="CodeFont">ALTER</span>](AlterTable.html) statement

 


