[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropView.html)

<a href="" id="Statements.DropView"></a>[]()DROP VIEW
=====================================================

The <span class="CodeFont">DROP VIEW</span> statement drops the specified view.

Syntax

``` FcnSyntax
DROP VIEW view-Name
```

view-Name

The name of the viewthat you want to drop from your database.

Example

``` Example
splice> DROP VIEW PlayerAges;
0 rows inserted/updated/deleted
```

Statement dependency system

Any statements referencing the view are invalidated on a <span class="CodeFont">DROP VIEW</span> statement.

See Also

-   [<span class="CodeFont">CREATE VIEW</span>](CreateView.html) statement
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause

 


