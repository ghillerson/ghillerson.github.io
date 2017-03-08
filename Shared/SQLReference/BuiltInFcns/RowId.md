[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/RowId.html)

[]()ROWID
=========

<span class="CodeFont">ROWID</span> is a <span class="ItalicFont">pseudocolumn</span> that uniquely defines a single row in a database table.

The term pseudocolumn is used because you can refer to <span class="CodeFont">ROWID</span> in the <span class="CodeFont">[SELECT](../Expressions/Select.html)</span> and <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clauses of a query as you would refer to a column stored in your database; the difference is you cannot insert, update, or delete <span class="CodeFont">ROWID</span> values.

The <span class="CodeFont">ROWID</span> value for a given row in a table remains the same for the life of the row, with one exception: the <span class="CodeFont">ROWID</span> may change if the table is an index organized table and you change its primary key.

[]()Syntax

``` FcnSyntax
ROWID
```

Usage

You can use a <span class="CodeFont">ROWID</span> value to refer to a row in a table in the <span class="CodeFont">[SELECT](../Expressions/Select.html)</span> and <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clauses of a query. These values have several valuable uses:

-   They are the fastest way to access a single row.
-   They are a built-in, unique identifier for every row in a table.
-   They provide information about how the rows in a table are stored.

Some important notes about <span class="CodeFont">ROWID</span> values:

-   Do not use <span class="CodeFont">ROWID</span> as the primary key of a table.
-   The <span class="CodeFont">ROWID</span> of a deleted row can later be reassigned to a new row.
-   A <span class="CodeFont">ROWID</span> value is associated with a table row when the row is created.
-   <span class="CodeFont">ROWID</span> values are unique within a table, but not necessarily unique within a database.
-   If you delete and re-import a row in a table, the <span class="CodeFont">ROWID</span> may change.
-   The <span class="CodeFont">ROWID</span> value for a row may change if the row is in an index organized table and you change the table's primary key.

Using ROWID with JDBC

You can access <span class="CodeFont">ROWID</span> with JDBC result sets; for example:

``` Example
() ResultSet.getRowId(int);
```

You can also use <span class="CodeFont">ROWID</span> in JDBC queries; for example:

``` Example
() CallableStatement.setRowId(int, RowId);
() PreparedStatement.setRowId(int, RowId);
```

Examples

This statement selects the unique row address and salary of all records in the employees database in the engineering department:

``` Example
splice> SELECT ROWID, DisplayName, Position 
   FROM Players 
   WHERE Team='Giants' and Position='OF';
   
ROWID                         |DISPLAYNAME             |POS&
------------------------------------------------------------
89                            |Greg Brown              |OF  
93                            |Jeremy Packman          |OF  
95                            |Jason Pratter           |OF  
99                            |Reed Lister             |OF  

4 rows selected
```

This statement updates column <span class="CodeFont">c</span> in all rows in which column <span class="CodeFont">b</span> equals <span class="CodeFont">10</span>:

``` Example
UPDATE mytable SET c=100 WHERE rowid=(SELECT rowid FROM mytable WHERE b=10);
```

See Also

-   <span class="CodeFont">[SELECT](../Expressions/Select.html)</span> expression
-   <span class="CodeFont">[SELECT](../Statements/Select.html)</span> statement
-   <span class="CodeFont">[UPDATE](../Statements/UpdateTable.html)</span> statement
-   <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause

 


