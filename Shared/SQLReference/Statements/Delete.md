[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Delete.html)

<a href="" id="Statements.Delete"></a>[]()DELETE
================================================

The <span class="CodeFont">DELETE</span> statement deletes records from a table.

Syntax

``` FcnSyntax
{
  DELETE FROM table-Name [[AS] correlation-Name]
    [WHERE clause]
}
```

table-Name

The name of the table from which you want to delete records.

correlation-Name

The optional alias (alternate name) for the table.

WHERE clause

The clause that specifies which record(s) to select for deletion.

Usage

The <span class="CodeFont">DELETE</span> statement removes all rows identified by the table name and <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause.

Examples

``` Example
splice> DELETE FROM Players WHERE Year(Birthdate) > 1990;
8 rows inserted/updated/deleted
```

Statement Dependency System

A searched delete statement depends on the table being updated, all of its conglomerates (units of storage such as heaps or indexes), and any other table named in the <span class="CodeFont">WHERE</span> clause. A <span class="CodeFont">[CREATE INDEX](CreateIndex.html)</span> or <span class="CodeFont">[DROP INDEX](DropIndex.html)</span> statement for the target table of a prepared searched delete statement invalidates the prepared searched delete statement.

A <span class="CodeFont">CREATE INDEX</span> or <span class="CodeFont">DROP INDEX</span> statement for the target table of a prepared positioned delete invalidates the prepared positioned delete statement.

See Also

-   [<span class="CodeFont">CREATE INDEX</span>](CreateIndex.html) statement
-   [<span class="CodeFont">DROP INDEX</span>](DropIndex.html) statement
-   [<span class="CodeFont">SELECT</span>](Select.html) statement
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


