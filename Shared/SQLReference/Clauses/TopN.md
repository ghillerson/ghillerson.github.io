[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/TopN.html)

[]()TOP n
=========

A <span class="CodeFont">TOP</span> clause, also called the <span class="CodeFont">TOP n</span> clause, limits the results of a query to the first <span class="CodeFont">n</span> result records.

Syntax

``` FcnSyntax
TOP [number] column-Name [, column-Name]*
```

number

Optional. An integer value that specifies the maximum number of rows to return from the query. If you omit this parameter, the default value of 1 is used.

column-Name

A column name, as described in the <span class="CodeFont">[Column Name](../Identifiers/IdentifierTypes.html#ColumnName)</span> topic.

You can specify <span class="CodeFont">\*</span> as the column name to represent all columns.

Examples

``` Example
splice> select * from toptest order by a;
A  |B  |C  |D
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

splice> select top * from toptest order by a;
A |B |C |D
--------------------------------------------------------------------------------
a1 |b1 |c1 |d1
1 row selected


splice> select top 3 a, b, c from toptest order by a;
A  |B  |C 
--------------------------------------------------------------------------------
a1 |b1 |c1
a2 |b2 |c2
a3 |b3 |c3
3 rows selected


splice> select top 10 a, b from toptest order by a;
A  |B 
--------------------------------------------------------------------------------
a1 |b1
a2 |b2
a3 |b3
a4 |b4
a5 |b5
a6 |b6
a7 |b7
a8 |b8
8 rows selected

splice> select top 4 * from toptest order by a offset 1 row;
A |B |C |D
--------------------------------------------------------------------------------
a2 |b2 |c2 |d2
a3 |b3 |c3 |d3
a4 |b4 |c4 |d4
a5 |b5 |c5 |d5
4 rows selected

splice> select top 4 * from toptest order by a offset 2 row;
A |B |C |D
--------------------------------------------------------------------------------
a3 |b3 |c3 |d3
a4 |b4 |c4 |d4
a5 |b5 |c5 |d5
a6 |b6 |c6 |d6
4 rows selected

splice> select top 4 * from toptest order by a offset -1 row ;
ERROR 2201X: Invalid row count for OFFSET, must be >= 0.


splice> select top 4 * from toptest order by a offset 10 row;
A |B |C |D
--------------------------------------------------------------------------------
0 rows selected
splice> select top -1 * from toptest;
ERROR 2201W: Row count for FIRST/NEXT/TOP must be >= 1 and row count for LIMIT must be >= 0.
```

See Also

-   <span class="CodeFont">[LIMIT n](Limit.html)</span> clause
-   <span class="CodeFont">[RESULT OFFSET](ResultOffset.html)</span> clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression

 


