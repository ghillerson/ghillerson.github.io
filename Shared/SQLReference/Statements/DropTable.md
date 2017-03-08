[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropTable.html)

<a href="" id="Statements.DropTable"></a>[]()DROP TABLE
=======================================================

The <span class="CodeFont">DROP TABLE</span> statement removes the specified table.

Syntax

``` FcnSyntax
DROP TABLE [IF EXISTS] table-Name
```

table-Name

The name of the schema that you want to drop from your database.

Statement dependency system

Indexes and constraints , constraints (primary, unique, check and references from the table being dropped) and triggers on the table are silently dropped.

Dropping a table invalidates statements that depend on the table. (Invalidating a statement causes it to be recompiled upon the next execution. See [Interaction with the dependency system](Interactions.html).)

Example

``` Example
splice> DROP TABLE Salaries;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">ALTER TABLE</span>](AlterTable.html) statement
-   <span class="CodeFont">[CREATE TABLE](CreateTable.html)</span> statement
-   [<span class="CodeFont">CONSTRAINT</span>](../Clauses/Constraint.html) clause

 


