[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/NextValueFor.html)

<a href="" id="Expressions.NextValueFor"></a>[]()NEXT VALUE FOR Expression
==========================================================================

The <span class="CodeFont">NEXT VALUE FOR</span> expression retrieves the next value from a sequence generator that was created with a [<span class="CodeFont">CREATE SEQUENCE</span> statement](../Statements/CreateSequence.html).

Syntax

``` FcnSyntax
NEXT VALUE FOR sequenceName
```

sequenceName

A sequence name is an identifier that can optionally be qualified by a schema name:

``` FcnSyntax
[ schemaName. ] SQLIdentifier
```

If <span class="ItalicFont">schemaName</span> is not provided, the current schema is the default schema. If a qualified sequence name is specified, the schema name cannot begin with the <span class="CodeFont">SYS. </span>prefix.

Usage

If this is the first use of the sequence generator, the generator returns its <span class="CodeFont">START</span> value. Otherwise, the <span class="CodeFont">INCREMENT</span> value is added to the previous value returned by the sequence generator. The data type of the value is the <span class="ItalicFont">dataType</span> specified for the sequence generator.

If the sequence generator wraps around, then one of the following happens:

-   If the sequence generator was created using the <span class="CodeFont">CYCLE</span> keyword, the sequence generator is reset to its <span class="CodeFont">START</span> value.
-   If the sequence generator was created with the default <span class="CodeFont">NO CYCLE</span> behavior, Splice Machine throws an exception.

In order to retrieve the next value of a sequence generator, you or your session's current role must have <span class="CodeFont">USAGE</span> privilege on the generator.

A <span class="CodeFont">NEXT VALUE FOR</span> expression may occur in the following places:

-   [<span class="CodeFont">SELECT</span> statement](../Statements/Select.html): As part of the expression defining a returned column in a <span class="CodeFont">SELECT</span> list
-   [<span class="CodeFont">VALUES</span> expression](Values.html): As part of the expression defining a column in a row constructor (<span class="CodeFont">VALUES</span> expression)
-   [<span class="CodeFont">UPDATE</span> statement](../Statements/UpdateTable.html); As part of the expression defining the new value to which a column is being set

The next value of a sequence generator is not affected by whether the user commits or rolls back a transaction which invoked the sequence generator.

Restrictions

Only one <span class="CodeFont">NEXT VALUE FOR</span> expression is allowed per sequence per statement.

The <span class="CodeFont">NEXT VALUE FOR</span> expression is not allowed in any statement which has a <span class="CodeFont">DISTINCT</span> or <span class="CodeFont">ORDER BY</span> expression.

A <span class="CodeFont">NEXT VALUE</span> expression <span class="BoldFont">may not appear</span> in any of these situations:

-   <span class="CodeFont">[CASE](Case.html)</span> expression
-   <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause
-   <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause
-   [Aggregate expression](../BuiltInFcns/Intro.WindowAggregrateFcns.html)
-   [Window functions](../BuiltInFcns/Intro.WindowAggregrateFcns.html)
-   <span class="CodeFont">[ROW\_NUMBER](../BuiltInFcns/RowNumber.html)</span> function
-   <span class="CodeFont">DISTINCT</span> select list

Examples

``` Example
VALUES (NEXT VALUE FOR order_id);

INSERT INTO re_order_table
  SELECT NEXT VALUE FOR order_id, order_date, quantity
  FROM orders
  WHERE back_order = 1;
            
UPDATE orders
  SET oid = NEXT VALUE FOR order_id
  WHERE expired = 1;
```

See Also

-   [<span class="CodeFont">CREATE SEQUENCE</span>](../Statements/CreateSequence.html) function
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement
-   [<span class="CodeFont">VALUES</span>](Values.html) expression
-   [<span class="CodeFont">UPDATE</span>](../Statements/UpdateTable.html) statement

 


