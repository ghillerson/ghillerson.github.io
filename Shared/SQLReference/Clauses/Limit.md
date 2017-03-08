[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Limit.html)

[]()LIMIT n
===========

A <span class="CodeFont">LIMIT n</span> clause, limits the results of a query to a specified number of records.

Syntax

``` FcnSyntax
'{' LIMIT {count} '}'
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You must surround the <span class="CodeFont">LIMIT</span> clause with left  and right curly brackets (<span class="CodeFont">{</span> and <span class="CodeFont">}</span>).

count

An integer value specifying the maximum number of rows to return from the query.

Examples

``` Example
splice> select * from limittest order by a;
A |B |C |D
--------------------------------------------------------------------------------
a1 |b1 |c1 |d1
a2 |b2 |c2 |d2
a3 |b3 |c3 |d3
a4 |b4 |c4 |d4
a5 |b5 |c5 |d5
a6 |b6 |c6 |d6
a7 |b7 |c7 |d7
a8 |b8 |c8 |d8
8 rows selected

splice> select * from limittest order by a {LIMIT 1};
A |B |C |D
--------------------------------------------------------------------------------
a1 |b1 |c1 |d1
1 row selected


splice> select * from limittest order by a {LIMIT 3};
A |B |C |D
--------------------------------------------------------------------------------
a1 |b1 |c1 |d1
a2 |b2 |c2 |d2
a3 |b3 |c3 |d3
3 rows selected


splice> select * from limittest order by a {LIMIT 10};
A |B |C |D
--------------------------------------------------------------------------------
a1 |b1 |c1 |d1
a2 |b2 |c2 |d2
a3 |b3 |c3 |d3
a4 |b4 |c4 |d4
a5 |b5 |c5 |d5
a6 |b6 |c6 |d6
a7 |b7 |c7 |d7
a8 |b8 |c8 |d8
8 rows selected
```

See Also

-   <span class="CodeFont">[RESULT OFFSET](ResultOffset.html)</span> clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   <span class="CodeFont">[TOP n](TopN.html)</span> clause

 


