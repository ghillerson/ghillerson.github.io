[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/IdentityValLocal.html)

<a href="" id="BuiltInFcns.IdentityValLocal"></a>[]()IDENTITY\_VAL\_LOCAL
=========================================================================

Splice Machine supports the <span class="CodeFont">IDENTITY\_VAL\_LOCAL</span> function.

Syntax:

``` FcnSyntax
IDENTITY_VAL_LOCAL ( )
```

The <span class="CodeFont">IDENTITY\_VAL\_LOCAL</span> function is a non-deterministic function that returns the most recently assigned value of an identity column for a connection, where the assignment occurred as a result of a single row <span class="CodeFont">INSERT</span> statement using a <span class="CodeFont">VALUES</span> clause.

The <span class="CodeFont">IDENTITY\_VAL\_LOCAL</span> function has no input parameters. The result is a <span class="CodeFont">DECIMAL (31,0)</span>, regardless of the actual data type of the corresponding identity column.

The value returned by the <span class="CodeFont">IDENTITY\_VAL\_LOCAL</span> function for a connection is the value assigned to the identity column of the table identified in the most recent single row <span class="CodeFont">INSERT</span> statement. The <span class="CodeFont">INSERT</span> statement must contain a <span class="CodeFont">VALUES</span> clause on a table containing an identity column. This function returns a <span class="CodeFont">null</span> value when a single row <span class="CodeFont">INSERT</span> statement with a <span class="CodeFont">VALUES</span> clause has not been issued for a table containing an identity column.

The result of the function is <span class="BoldFont">not</span> affected by the following:

-   A single row <span class="CodeFont">INSERT</span> statement with a <span class="CodeFont">VALUES</span> clause for a table without an identity column
-   A multiple row <span class="CodeFont">INSERT</span> statement with a <span class="CodeFont">VALUES</span> clause
-   An <span class="CodeFont">INSERT</span> statement with a full <span class="CodeFont">SELECT</span>

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If a table with an identity column has an <span class="CodeFont">INSERT</span> trigger defined that inserts into another table with another identity column, then the <span class="CodeFont">IDENTITY\_VAL\_LOCAL()</span> function will return the generated value for the statement table, and not for the table modified by the trigger.

Examples

``` Example
splice> CREATE TABLE t1(c1 INT GENERATED ALWAYS AS IDENTITY, c2 INT);
0 rows inserted/updated/deleted


splice> INSERT INTO t1(c2) VALUES(8);
1 row inserted/updated/deleted


splice> VALUES IDENTITY_VAL_LOCAL();
1 
-------------------------------
1                              
1 row selected
```

``` Example
splice> SELECT IDENTITY_VAL_LOCAL()+1, IDENTITY_VAL_LOCAL()-1 FROM t1;
1                                |2                          
-------------------------------------------------------------------
2                                |0                                
1 row selected
```

``` Example
splice> INSERT INTO t1(c2) VALUES (IDENTITY_VAL_LOCAL());
1 row inserted/updated/deleted


splice> SELECT * FROM t1;
C1             |C2             
-------------------------------
1              |8              
2              |1              
2 rows selected
```

``` Example
splice> VALUES IDENTITY_VAL_LOCAL();
1                        
-------------------------------
2                              
1 row selected


splice> INSERT INTO t1(c2) VALUES (8), (9);
2 rows inserted/updated/deleted

          -- multi-values insert, return value of the function should not change

splice> VALUES IDENTITY_VAL_LOCAL();
1                        
-------------------------------
2                              
1 row selected
```

``` Example
splice> SELECT * FROM t1;
C1             |C2             
-------------------------------
1              |8              
2              |1              
3              |8              
4              |9              
4 rows selected
```

``` Example
splice> INSERT INTO t1(c2) SELECT c1 FROM t1;
4 rows inserted/updated/deleted

           -- insert with sub-select, return value should not change
splice> VALUES IDENTITY_VAL_LOCAL();
1                        
-------------------------------
2                              
1 row selected
```

``` Example
splice> SELECT * FROM t1;
C1             |C2             
-------------------------------
1              |8              
2              |1              
3              |8              
4              |9              
5              |1              
6              |2              
7              |3              
8              |4              
-------------------------------
8 rows selected 
```

 


