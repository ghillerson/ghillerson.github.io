[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Except.html)

[]()EXCEPT
==========

The <span class="CodeFont">EXCEPT</span> operator combines the result set of two or more similar <span class="CodeFont">SELECT</span> queries, returning the results from the first query that do not appear in the results of the second query.

This is a new topic in the Splice Machine documentation.

If your find any problems with this page, please file a JIRA bug, or email [docs@splicemachine.com](mailto:docs@splicemachine.com?subject=Problem%20with%20docs%20page "Click to send an email to docs@splicemachine.com")

Syntax

``` FcnSyntax
SELECT expression EXCEPT [ DISTINCT | ALL ] SELECT expression
   [ EXCEPT [DISTINCT | ALL] SELECT expression ]*
```

SELECT expression

A <span class="CodeFont">SELECT</span> expression that does not include an <span class="CodeFont">ORDER BY</span> clause.

If you include an <span class="CodeFont">ORDER BY</span> clause, that clause applies to the intersection operation.

DISTINCT

(Optional). Indicates that only distinct (non-duplicate) rows from the queries are included. This is the default.

ALL

(Optional). Indicates that all rows from the queries are included, including duplicates. With <span class="CodeFont">ALL</span>, a row that has m duplicates in the left table and n duplicates in the right table will appear <span class="CodeFont">max(m-n,0)</span> times in the result set.

Usage

Each <span class="CodeFont">SELECT</span> statement in the operation must contain the same number of columns, with similar data types, in the same order. Although the number, data types, and order of the fields in the select queries that you combine in an <span class="CodeFont">EXCEPT</span> clause must correspond, you can use expressions, such as calculations or subqueries, to make them correspond.

When comparing column values for determining <span class="CodeFont">DISTINCT</span> rows, two <span class="CodeFont">NULL</span> values are considered equal.

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
splice> SELECT id,i1,i2 FROM t1 EXCEPT SELECT id,i1,i2 FROM t2 ORDER BY id,i1,i2;
ID         |I1         |I2         
-----------------------------------
4          |1          |3          
3          |1          |3          
6          |NULL       |NULL       

3 rows selected
```

``` Example
splice> 
SELECT i1,i2 FROM t1
 EXCEPT 
SELECT i1,i2 FROM t2 where id = -1 ORDER BY 1,2;
I1         |I2         
-----------------------
NULL       |NULL       
1          |3          
1          |2          
1          |1          

4 rows selected
```

``` Example
splice> 
SELECT i1,i2 FROM t1 where id = -1
 EXCEPT 
SELECT i1,i2 FROM t2 ORDER BY 1,2;
I1         |I2         
-----------------------

0 rows selected
```

See Also

-   [Union clause](Union.html)

 


