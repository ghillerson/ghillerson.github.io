[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Union.html)

[]()UNION
=========

The <span class="CodeFont">UNION</span> operator combines the result set of two or more similar <span class="CodeFont">SELECT</span> queries, and returns distinct rows.

This is a new topic in the Splice Machine documentation.

If your find any problems with this page, please file a JIRA bug, or email [docs@splicemachine.com](mailto:docs@splicemachine.com?subject=Problem%20with%20docs%20page "Click to send an email to docs@splicemachine.com")

Syntax

``` FcnSyntax
SELECT expression UNION [ DISTINCT | ALL ] SELECT expression 
   [ UNION [DISTINCT | ALL] SELECT expression ]*
```

SELECT expression

A <span class="CodeFont">SELECT</span> expression that does not include an <span class="CodeFont">ORDER BY</span> clause.

If you include an <span class="CodeFont">ORDER BY</span> clause, that clause applies to the intersection operation.

DISTINCT

(Optional). Indicates that only distinct (non-duplicate) rows from the queries are included. This is the default.

ALL

(Optional). Indicates that all rows from the queries are included, including duplicates.

Usage

Each <span class="CodeFont">SELECT</span> statement in the union must contain the same number of columns, with similar data types, in the same order. Although the number, data types, and order of the fields in the select queries that you combine in a <span class="CodeFont">UNION</span> clause must correspond, you can use expressions, such as calculations or subqueries, to make them correspond.

Each <span class="CodeFont">UNION</span> keyword combines the <span class="CodeFont">SELECT</span> statements that immediately precede and follow it. If you use the <span class="CodeFont">ALL</span> keyword with some of the <span class="CodeFont">UNION</span> keywords in your query, but not with others, the results will include duplicate rows from the pairs of <span class="CodeFont">SELECT</span> statements that are combined by using <span class="CodeFont">UNION ALL</span>, but will not include duplicate rows from the <span class="CodeFont">SELECT</span> statements that are combined by using <span class="CodeFont">UNION</span> without the <span class="CodeFont">ALL</span> keyword.

Results

A result set.

Examples

``` Example
CREATE TABLE t1( id INTEGER NOT NULL PRIMARY KEY, 
                 i1 INTEGER, i2 INTEGER,
                 c10 char(10), c30 char(30), tm time);
 
CREATE TABLE t2( id INTEGER NOT NULL PRIMARY KEY,
                 i1 INTEGER, i2 INTEGER,
                 vc20 varchar(20), d double, dt date);
 
INSERT INTO t1(id,i1,i2,c10,c30) VALUES
  (1,1,1,'a','123456789012345678901234567890'),
  (2,1,2,'a','bb'),
  (3,1,3,'b','bb'),
  (4,1,3,'zz','5'),
  (5,NULL,NULL,NULL,'1.0'),
  (6,NULL,NULL,NULL,'a');
  
INSERT INTO t2(id,i1,i2,vc20,d) VALUES
  (1,1,1,'a',1.0),
  (2,1,2,'a',1.1),
  (5,NULL,NULL,'12345678901234567890',3),
  (100,1,3,'zz',3),
  (101,1,2,'bb',NULL),
  (102,5,5,'',NULL),
  (103,1,3,' a',NULL),
  (104,1,3,'NULL',7.4);
```

``` Example
splice> 
SELECT id,i1,i2 FROM t1
 UNION
SELECT id,i1,i2 FROM t2 ORDER BY id,i1,i2;
ID         |I1         |I2         
-----------------------------------
1          |1          |1          
2          |1          |2          
3          |1          |3          
4          |1          |3          
5          |NULL       |NULL       
6          |NULL       |NULL       
100        |1          |3          
101        |1          |2          
102        |5          |5          
103        |1          |3          
104        |1          |3          

11 rows selected
```

``` Example
splice> 
SELECT id,i1,i2 FROM t1
 UNION ALL
SELECT id,i1,i2 FROM t2 ORDER BY id,i1,i2;
ID         |I1         |I2         
-----------------------------------
1          |1          |1          
1          |1          |1          
2          |1          |2          
2          |1          |2          
3          |1          |3          
4          |1          |3          
5          |NULL       |NULL       
5          |NULL       |NULL       
6          |NULL       |NULL       
100        |1          |3          
101        |1          |2          
102        |5          |5          
103        |1          |3          
104        |1          |3          

14 rows selected
```

See Also

-   [Except clause](Except.html)

 


