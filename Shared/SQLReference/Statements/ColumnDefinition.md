[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/ColumnDefinition.html)

<a href="" id="Statements.ColumnDefinition"></a>[]()column-definition
=====================================================================

``` FcnSyntax
Simple-column-Name
   [ DataType ]
   [ Column-level-constraint ]*
   [ [ WITH ] DEFAULT DefaultConstantExpression
     | generated-column-spec 
     | generation-clause 
   ] 
   [ Column-level-constraint ]*
```

DataType

Must be specified unless you specify a generation-clause, in which case the type of the generated column is that of the generation-clause.

If you specify both a <span class="ItalicFont">DataType</span> and a <span class="ItalicFont">generation-clause</span>, the type of the <span class="ItalicFont">generation-clause</span> must be assignable to <span class="ItalicFont">DataType</span>

Column-level-constraint

See the [<span class="CodeFont">CONSTRAINT</span> clause](../Clauses/Constraint.html) documentation.

DefaultConstantExpression<a href="" id="ColumnDefault"></a>

For the definition of a default value, a DefaultConstantExpression is an expression that does not refer to any table. It can include constants, date-time special registers, current schemas, and null:

``` FcnSyntax
DefaultConstantExpression:
   NULL
 | CURRENT { SCHEMA | SQLID }
 | DATE
 | TIME
 | TIMESTAMP
 | CURRENT DATE | CURRENT_DATE
 | CURRENT TIME | CURRENT_TIME
 | CURRENT TIMESTAMP | CURRENT_TIMESTAMP
 | literal
```

The values in a DefaultConstantExpression must be compatible in type with the column, but a DefaultConstantExpression has the following additional type restrictions:

-   If you specify <span class="CodeFont">CURRENT SCHEMA</span> or <span class="CodeFont">CURRENT SQLID</span>, the column must be a character column whose length is at least 128.
-   If the column is an integer type, the default value must be an integer literal.
-   If the column is a decimal type, the scale and precision of the default value must be within those of the column.

Example

This example creates a table and uses two column definitions.

``` Example
splice> CREATE TABLE myTable (ID INT NOT NULL, NAME VARCHAR(32) );
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CONSTRAINT</span>](../Clauses/Constraint.html) clause

 


