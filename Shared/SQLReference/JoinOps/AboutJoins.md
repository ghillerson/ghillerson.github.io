[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/AboutJoins.html)

<a href="" id="JoinOps.AboutJoins"></a>[]()About Join Operations
================================================================

The <span class="CodeFont">JOIN</span> operations, which are among the possible <span class="ItalicFont">[TableExpression](../Expressions/Table.html)s</span> in a [<span class="CodeFont">FROM</span> clause](../Clauses/From.html), perform joins between two tables.

Syntax

``` FcnSyntax
JOIN Operation
```

The following table describes the <span class="CodeFont">JOIN</span> operations:

| Join Operation   | Description                                                                                                                                                                   |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| INNER JOIN       | Specifies a join between two tables with an explicit join clause.                                                                                                             |
| LEFT OUTER JOIN  | Specifies a join between two tables with an explicit join clause, preserving unmatched rows from the first table.                                                             |
| RIGHT OUTER JOIN | Specifies a join between two tables with an explicit join clause, preserving unmatched rows from the second table.                                                            |
| CROSS JOIN       | Specifies a join that produces the Cartesian product of two tables. It has no explicit join clause.                                                                           |
| NATURAL JOIN     | Specifies an inner or outer join between two tables. It has no explicit join clause. Instead, one is created implicitly using the common columns from the two tables.         
                                                                                                                                                                                                   
                    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine does not currently support <span class="CodeFont">NATURAL SELF JOIN</span> operations.  |

In all cases, you can specify additional restrictions on one or both of the tables being joined in outer join clauses or in the [<span class="CodeFont">WHERE</span> clause](../Clauses/Where.html).

Usage

Note that you can also perform a join between two tables using an explicit equality test in a [<span class="CodeFont">WHERE</span> clause](../Clauses/Where.html), such as:

``` Example
WHERE t1.col1 = t2.col2.
```

See Also

-   [<span class="CodeFont">FROM</span>](../Clauses/From.html) clause
-   [JOIN operations](Intro.JoinOps.html) 
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expressions
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


