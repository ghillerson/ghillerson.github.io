[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/RenameColumn.html)

<a href="" id="Statements.RenameColumn"></a>[]()RENAME COLUMN
=============================================================

Use the <span class="CodeFont">RENAME COLUMN</span> statement to rename a column in a table.

The <span class="CodeFont">RENAME COLUMN</span> sactatement allows you to rename an existing column in an existing table in any schema (except the schema <span class="CodeFont">SYS</span>).

Syntax

``` FcnSyntax
RENAME COLUMN table-Name.simple-Column-Name
  TO simple-Column-Name
```

table-Name

The name of the table containing the column to rename.

simple-Column-Name

The name of the column to be renamed.

simple-Column-Name

The new name for the column.

Usage Notes

To rename a column, you must either be the database owner or the table owner.

To perform other table alterations, see the [<span class="CodeFont">ALTER TABLE</span> statement](AlterTable.html).

<span class="autonumber"><span class="noteAutoNum">RESTRICTION:  </span></span>If a view, <span>trigger, </span>check constraint, or <span class="ItalicFont">[generation-clause](GenerationClause.html)</span> of a generated column references the column, an attempt to rename it will generate an error.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If there is an index defined on the column, the column can still be renamed; the index is automatically updated to refer to the column by its new name.

Examples

To rename the <span class="CodeFont">Birthdate</span> column in table <span class="CodeFont">Players</span> to <span class="CodeFont">BornDate</span>, use the following syntax:

``` Example
splice> RENAME COLUMN Players.Birthdate TO BornDate;
0 rows inserted/updated/deleted
```

If you want to modify a column's data type, you can combine <span class="CodeFont">ALTER TABLE</span>, <span class="CodeFont">UPDATE</span>, and <span class="CodeFont">RENAME COLUMN</span> using these steps, as show in the example below:

1.  Add a new column to the table with the new data type
2.  Copy the values from the "old" column to the new column with an UPDATE statement.
3.  Drop the "old" column.
4.  Rename the new column with the old column's name.

``` Example
splice> ALTER TABLE Players ADD COLUMN NewPosition VARCHAR(8);
0 rows inserted/updated/deleted

splice> UPDATE Players SET NewPosition = Position;
0 rows inserted/updated/deleted

splice> ALTER TABLE Players DROP COLUMN Position;
0 rows inserted/updated/deleted

splice> RENAME COLUMN Players.NewPosition TO Position;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">ALTER</span>](AlterTable.html) statement

 


