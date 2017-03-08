[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/UpdateTable.html)

<a href="" id="Statements.Update"></a>[]()UPDATE
================================================

Use the <span class="CodeFont">UPDATE</span> statement to update existing records in a table.

Syntax

``` FcnSyntax
{
 UPDATE table-Name 
   [[AS] correlation-Name]
   SET column-Name = Value
       [ , column-Name = Value} ]*
   [WHERE clause]
} 
```

table-Name

The name of the table to update.

correlation-Name

An optional correlation name for the update.

column-Name = Value

Sets the value of the named column to the named value in any records .

<span class="ItalicFont">Value</span> is either an <span class="ItalicFont">[Expression](../Expressions/AboutExpressions.html)</span> or the literal <span class="CodeFont">DEFAULT</span>. If you specify <span class="CodeFont">DEFAULT</span> for a column's value, the value is set to the default defined for the column in the table.

The <span class="CodeFont">DEFAULT</span> literal is the only value that you can directly assign to a generated column. Whenever you alter the value of a column referenced by the <span class="ItalicFont">[generation-clause](GenerationClause.html)</span> of a generated column, Splice Machine recalculates the value of the generated column.

WHERE clause

Specifies the records to be updated.

Example

This example updates the Birthdate value for a specific player:

``` Example
splice> UPDATE Players 
   SET Birthdate='03/27/1987' 
   WHERE DisplayName='Buddy Painter';
1 row inserted/updated/deleted
```

This example updates the team name associated with all players on the <span class="CodeFont">Giants</span> team:

``` Example
splice> UPDATE Players
   SET Team='SFGiants'
   WHERE Team='Giants';
48 rows inserted/updated/deleted
```

Statement dependency system

A searched update statement depends on the table being updated, all of its conglomerates (units of storage such as heaps or indexes), all of its constraints, and any other table named in the <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause or <span class="CodeFont">SET</span> expressions. A <span class="CodeFont">[CREATE](CreateTable.html)</span> or <span class="CodeFont">[DROP INDEX](DropIndex.html)</span> statement or an <span class="CodeFont">[ALTER TABLE](AlterTable.html)</span> statement for the target table of a prepared searched update statement invalidates the prepared searched update statement.

A <span class="CodeFont">CREATE</span> or <span class="CodeFont">DROP INDEX</span> statement or an <span class="CodeFont">ALTER TABLE</span> statement for the target table of a prepared positioned update invalidates the prepared positioned update statement.

Dropping an alias invalidates a prepared update statement if the latter statement uses the alias.

Dropping or adding triggers on the target table of the update invalidates the update statement.

See Also

-   [<span class="CodeFont">ALTER TABLE</span>](AlterTable.html)statement
-   [<span class="CodeFont">CONSTRAINT</span>](../Clauses/Constraint.html)clause
-   [<span class="CodeFont">CREATE TABLE</span>](CreateTable.html)statement
-   <span class="CodeFont">[CREATE TRIGGER](CreateTrigger.html)</span>
-   [<span class="CodeFont">DROP INDEX</span>](DropIndex.html)statement
-   <span class="CodeFont">[DROP TRIGGER](DropTrigger.html)</span>
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html)clause

 


