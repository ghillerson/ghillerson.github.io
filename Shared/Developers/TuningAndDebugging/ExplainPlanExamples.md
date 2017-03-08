[Open topic with navigation](../../../index.html#Shared/Developers/TuningAndDebugging/ExplainPlanExamples.html)

[]()Explain Plan Examples
=========================

This topic contains the following examples of using the <span class="CodeFont">explain</span> command to display the execution plan for a statement, including the following examples:

-   [TableScan Examples](#TableSca)
-   [IndexScan Examples](#IndexSca)
-   [Projection and Restriction Examples](#Projecti)
-   [Index Lookup](#Index)
-   [Join Example](#Join)
-   [Union Example](#Union)
-   [Order By Example](#Order)
-   [Aggregation Operation Examples](#Aggregat)
-   [Subquery Example](#Subquery)

The format and meaning of the common fields in the output plans shown here is found in the previous topic, [About Explain Plan](ExplainPlan.html).

[]()TableScan Examples
----------------------

This example show a plan for a <span class="CodeFont">TableScan</span> operation that has no qualifiers, known as a <span class="ItalicFont">raw scan</span>:

``` AppCommand
splice> explain select * from sys.systables;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=3,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=2,totalCost=8.594,outputRows=20,outputHeapSize=3.32 KB,partitions=1)
    ->  TableScan[SYSTABLES(48)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=3.32 KB,partitions=1)

3 rows selected
```

This example show a plan for a <span class="CodeFont">TableScan</span> operation that does have qualifiers::

``` AppCommand
splice> explain select * from sys.systables --SPLICE-PROPERTIES index=NULL
   where tablename='SYSTABLES';

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=3,rows=18,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=2,totalCost=8.54,outputRows=18,outputHeapSize=2.988 KB,partitions=1)
    ->  TableScan[SYSTABLES(48)](n=1,totalCost=4.054,outputRows=18,outputHeapSize=2.988 KB,partitions=1,preds=[(TABLENAME[0:2] = SYSTABLES)])

3 rows selected
```

### Nodes

-   The plan labels this operation as <span class="CodeFont">TableScan\[</span><span class="ItalicFont">tableId</span>(<span class="ItalicFont">conglomerateId</span>)<span class="CodeFont">\]</span>:

    -   <span class="ItalicFont">tableId</span> is the name of the table, in the form <span class="CodeFont">schemaName '.' tableName</span>.
    -   <span class="ItalicFont">conglomerateId</span> is an ID that is unique to every HBase table; this value is used internally, and can be used for certain administrative tasks
-   The <span class="CodeFont">preds</span> field includes qualifiers that were pushed down to the base table.

[]()IndexScan Examples
----------------------

This example show a plan for an <span class="CodeFont">IndexScan</span> operation that has no predicates:

``` AppCommand
splice> explain select tablename from sys.systables; --covering index

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=3,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=2,totalCost=8.31,outputRows=20,outputHeapSize=560 B,partitions=1)
    ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=560 B,partitions=1,baseTable=SYSTABLES(32))

3 rows selected
```

This example shows a plan for an <span class="CodeFont">IndexScan</span> operation that contains predicates:

``` AppCommand
splice> explain select tablename from sys.systables --SPLICE-PROPERTIES index=SYSTABLES_INDEX1
        where tablename = 'SYSTABLES';

Plan
-------------------------------------------------------------------------------------------------Cursor(n=3,rows=18,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=2,totalCost=8.272,outputRows=18,outputHeapSize=432 B,partitions=1)
    ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.049,outputRows=18,outputHeapSize=432 B,partitions=1,baseTable=SYSTABLES(48),preds=[(TABLENAME[0:1] = SYSTABLES)])

3 rows selected
```

### Nodes

-   The plan labels this operation as <span class="CodeFont">IndexScan\[</span><span class="ItalicFont">indexId(conglomerateId)</span><span class="CodeFont">\]</span>:

    -   <span class="ItalicFont">indexId</span> is the name of the index
    -   <span class="ItalicFont">conglomerateId</span> is an ID that is unique to every HBase table; this value is used internally, and can be used for certain administrative tasks
-   The <span class="CodeFont">preds</span> field includes qualifiers that were pushed down to the base table.

[]()Projection and Restriction Examples
---------------------------------------

This example show a plan for a <span class="CodeFont">Projection</span> operation:

``` AppCommand
splice> explain select tablename || 'hello' from sys.systables;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=4,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=3,totalCost=8.302,outputRows=20,outputHeapSize=480 B,partitions=1)
    ->  ProjectRestrict(n=2,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1)
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48))

4 rows selected
```

This example shows a plan for a <span class="CodeFont">Restriction</span> operation:

``` AppCommand
splice> explain select tablename from sys.systables
        where tablename like '%SYS%';

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=4,rows=10,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=3,totalCost=8.178,outputRows=10,outputHeapSize=240 B,partitions=1)
    ->  ProjectRestrict(n=2,totalCost=4.054,outputRows=10,outputHeapSize=240 B,partitions=1,preds=[like(TABLENAME[0:1], %SYS%)])
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=240 B,partitions=1,baseTable=SYSTABLES(48))

4 rows selected
```

### Nodes

-   The plan labels both projection and restriction operations as <span class="CodeFont">ProjectRestrict</span>. which can contain both <span class="ItalicFont">projections</span> and <span class="ItalicFont">non-qualifier restrictions</span>. A <span class="ItalicFont">non-qualifier restriction</span> is a predicate that cannot be pushed to the underlying table scan.

[]()Index Lookup
----------------

This example shows a plan for an <span class="CodeFont">IndexLookup</span> operation:

``` AppCommand
splice> explain select * from SYS.SYSTABLES --SPLICE-PROPERTIES index=SYSTABLES_INDEX1
where tablename = 'SYSTABLES';;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=4,rows=18,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=3,totalCost=177.265,outputRows=18,outputHeapSize=921.586 KB,partitions=1)
    ->  IndexLookup(n=2,totalCost=78.715,outputRows=18,outputHeapSize=921.586 KB,partitions=1)
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=6.715,outputRows=18,outputHeapSize=921.586 KB,partitions=1,baseTable=SYSTABLES(48),preds=[(TABLENAME[1:2] = SYSTABLES)])
```

Nodes

-   The plan labels the operation as <span class="CodeFont">IndexLookup</span>; you may see this labeled as an <span class="CodeFont">IndexToBaseRow</span> operation elsewhere.
-   Plans for <span class="CodeFont">IndexLookup</span> operations do not contain any special fields.

[]()Join Example
----------------

This example shows a plan for a <span class="CodeFont">Join</span> operation:

``` AppCommand
splice> explain select * from sys.systables t, sys.sysschemas s
        where t.schemaid =s.schemaid;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=5,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=4,totalCost=21.728,outputRows=20,outputHeapSize=6.641 KB,partitions=1)
    ->  BroadcastJoin(n=3,totalCost=12.648,outputRows=20,outputHeapSize=6.641 KB,partitions=1,preds=[(T.SCHEMAID[4:4] = S.SCHEMAID[4:8])])
      ->  TableScan[SYSSCHEMAS(32)](n=2,totalCost=4.054,outputRows=20,outputHeapSize=6.641 KB,partitions=1)
      ->  TableScan[SYSTABLES(48)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=3.32 KB,partitions=1)

5 rows selected
```

Nodes

-   The plan labels the operation using the <span class="ItalicFont">join type</span> followed by <span class="CodeFont">Join</span>; the possible values are:

    -   BroadcastJoin
    -   MergeJoin
    -   MergeSortJoin
    -   NestedLoopJoin
    -   OuterJoin
-   The plan may include a <span class="CodeFont">preds</span> field, which lists the join predicates.
-   <span class="CodeFont">NestedLoopJoin</span> operations do not include a <span class="CodeFont">preds</span> field; instead, the predicates are listed in either a <span class="CodeFont">ProjectRestrict</span> or in the underlying scan.
-   The right side of the <span class="ItalicFont">Join</span> operation is listed first, followed by the left side of the join.

### Outer Joins

An <span class="ItalicFont">outer join</span> does not display it as a separate strategy in the plan; instead, it is treated a <span class="ItalicFont">postfix</span> for the strategy that's used. For example, if you are using a Broadcast join, and it's a left outer join, then you'll see <span class="CodeFont">BroadcastLeftOuterJoin</span>. Here's an example:

``` AppCommand
explain select s.schemaname,t.tablename from sys.sysschemas s left outer join sys.systables t
> on s.schemaid = t.schemaid;
Plan
-------------------------------------------------------------------------------------------------
Cursor(n=6,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=5,totalCost=348.691,outputRows=20,outputHeapSize=2 MB,partitions=1)
    ->  ProjectRestrict(n=4,totalCost=130.579,outputRows=20,outputHeapSize=2 MB,partitions=1)
      ->  BroadcastLeftOuterJoin(n=3,totalCost=130.579,outputRows=20,outputHeapSize=2 MB,partitions=1,preds=[(S.SCHEMAID[4:1] = T.SCHEMAID[4:4])])
        ->  IndexScan[SYSTABLES_INDEX1(145)](n=2,totalCost=7.017,outputRows=20,outputHeapSize=2 MB,partitions=1,baseTable=SYSTABLES(48))
        ->  TableScan[SYSSCHEMAS(32)](n=1,totalCost=7.516,outputRows=20,outputHeapSize=1023.984 KB,partitions=1)
```

[]()Union Example
-----------------

This example shows a plan for a <span class="CodeFont">Union</span> operation:

``` AppCommand
splice> explain select tablename from sys.systables t union all select schemaname from sys.sysschemas;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=5,rows=40,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=4,totalCost=16.668,outputRows=40,outputHeapSize=1.094 KB,partitions=1)
    ->  Union(n=3,totalCost=12.356,outputRows=40,outputHeapSize=1.094 KB,partitions=1)
      ->  IndexScan[SYSSCHEMAS_INDEX1(209)](n=2,totalCost=4.054,outputRows=20,outputHeapSize=1.094 KB,partitions=1,baseTable=SYSSCHEMAS(32))
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48))

5 rows selected
```

Nodes

-   The right side of the <span class="CodeFont">Union</span> is listed first, followed by the left side of the union,

[]()Order By Example
--------------------

This example shows a plan for an order by operation:

``` AppCommand
splice> explain select tablename from sys.systables order by tablename desc;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=4,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=3,totalCost=16.604,outputRows=20,outputHeapSize=480 B,partitions=1)
    ->  OrderBy(n=2,totalCost=12.356,outputRows=20,outputHeapSize=480 B,partitions=1)
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48))

4 rows selected
```

Nodes

-   The plan labels this operation as <span class="CodeFont">OrderBy</span>.

[]()Aggregation Operation Examples
----------------------------------

This example show a plan for a grouped aggregate operation:

``` AppCommand
splice> explain select tablename, count(*) from sys.systables group by tablename;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=6,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=5,totalCost=12.568,outputRows=20,outputHeapSize=480 B,partitions=16)
    ->  ProjectRestrict(n=4,totalCost=8.32,outputRows=20,outputHeapSize=480 B,partitions=16)
      ->  GroupBy(n=3,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1)
        ->  ProjectRestrict(n=2,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1)
          ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48))

6 rows selected)
```

This example shows a plan for a scalar aggregate operation:

``` AppCommand
splice> explain select count(*) from sys.systables;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=6,rows=1,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=5,totalCost=8.797,outputRows=1,outputHeapSize=0 B,partitions=1)
    ->  ProjectRestrict(n=4,totalCost=4.257,outputRows=1,outputHeapSize=0 B,partitions=1)
      ->  GroupBy(n=3,totalCost=4.054,outputRows=20,outputHeapSize=3.32 KB,partitions=1)
        ->  ProjectRestrict(n=2,totalCost=4.054,outputRows=20,outputHeapSize=3.32 KB,partitions=1)
          ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=3.32 KB,partitions=1,baseTable=SYSTABLES(48))

6 rows selected
```

Nodes

-   The plan labels both grouped and scaled aggregate operations as <span class="CodeFont">GroupBy</span>.

[]()Subquery Example
--------------------

This example shows a plan for a <span class="CodeFont">SubQuery</span> operation:

``` AppCommand
splice> explain select tablename, (select tablename from sys.systables t2 where t2.tablename = t.tablename)from sys.systables t;

Plan
-------------------------------------------------------------------------------------------------
Cursor(n=6,rows=20,updateMode=READ_ONLY (1),engine=control)
  ->  ScrollInsensitive(n=5,totalCost=8.302,outputRows=20,outputHeapSize=480 B,partitions=1)
    ->  ProjectRestrict(n=4,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1)
      ->  Subquery(n=3,totalCost=12.55,outputRows=20,outputHeapSize=480 B,partitions=1,correlated=true,expression=true,invariant=true)
        ->  IndexScan[SYSTABLES_INDEX1(145)](n=2,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48),preds=[(T2.TABLENAME[0:1] = T.TABLENAME[4:1])])
      ->  IndexScan[SYSTABLES_INDEX1(145)](n=1,totalCost=4.054,outputRows=20,outputHeapSize=480 B,partitions=1,baseTable=SYSTABLES(48))

6 rows selected
```

Nodes

-   Subqueries are listed as a second query tree, whose starting indentation level is the same as the <span class="CodeFont">ProjectRestrict</span> operation that <span class="ItalicFont">owns</span> the subquery.
-   Includes a <span class="ItalicFont">correlated</span> field, which specifies whether or not the query is treated as correlated or uncorrelated.
-   Includes an <span class="ItalicFont">expression</span> field, which specifies whether or not the subquery is an expression.
-   Includes an <span class="ItalicFont">invariant</span> field, which indicates whether the subquery is invariant.

See Also
--------

-   [About Explain Plan](ExplainPlan.html)

 


