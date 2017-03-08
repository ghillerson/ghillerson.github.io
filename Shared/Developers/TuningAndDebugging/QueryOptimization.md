[Open topic with navigation](../../../index.html#Shared/Developers/TuningAndDebugging/QueryOptimization.html)

[]()Optimizing Splice Machine Queries
=====================================

This topic introduces you to Splice Machine query optimization techniques, including information about executing SQL expressions without a table context, and using optimization hints.

Introduction to Query Optimization
----------------------------------

Here are a few mechanisms you can use to optimize your Splice Machine queries:

| Optimization Mechanism                                         | Description                                                                                                                                                                                                                                                               |
|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Use Explain Plan                                               | You can use the Splice Machine Explain Plan facility to display the execution plan for a statement without actually executing the statement. You can use Explain Plan to help determine options such as which join strategy to use or which index to select.              
                                                                                                                                                                                                                                                                                                                                             
                                                                  See the [About Explain Plan](ExplainPlan.html) topic in our <span class="ItalicFont">Administrator's Guide</span>.                                                                                                                                                         |
| Use Statistics                                                 | Your database administrator can refine which statistics are collected on your database, which in turn enhances the operation of the query optimizer. See the [Using Statistics](UsingStatistics.html) topic in our <span class="ItalicFont">Administrator's Guide</span>. |
| Use <span class="CodeFont">WHERE</span> clauses                | Use a <span class="CodeFont">WHERE</span> clause in your queries to restrict how much data is scanned.                                                                                                                                                                    |
| Use indexes                                                    | You can speed up a query by having an index on the criteria used in the <span class="CodeFont">WHERE</span> clause, or if the <span class="CodeFont">WHERE</span> clause is using a primary key.                                                                          
                                                                                                                                                                                                                                                                                                                                             
                                                                  Composite indexes work well for optimizing queries.                                                                                                                                                                                                                        |
| Use Splice Machine <span class="ItalicFont">query hints</span> | The Splice Machine query optimizer allows you to [provide hints](#Using) to help in the optimization process.                                                                                                                                                             |

[]()[]()Using Select Without a Table
------------------------------------

Sometimes you want to execute SQL scalar expressions without having a table context. For example, you might want to create a query that evaluates an expression and returns a table with a single row and one column. Or you might want to evaluate a list of comma-separated expressions and return a table with a single row and multiple columns — one for each expression.

In Splice Machine, you can execute queries without a table by using the <span class="CodeFont">sysibm.sysdummy1</span> dummy table. Here's the syntax:

``` FcnSyntax
select expression FROM sysibm.dummy1
```

And here's an example:

``` Example
splice> select 1+ 1 from sysibm.sysdummy1; 
```

[]()Using Splice Machine Query Hints
------------------------------------

You can use <span class="ItalicFont">hints</span> to help the Splice Machine query interface optimize your database queries.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The Splice Machine optimizer is constantly being improved, and new hint types sometimes get added. One recent addition is the ability to specify that a query should be run on (or not on) Spark, if possible.

### Types of Hints

There are different kinds of hints you can supply, each of which is described in a section below; here's a summary:

| Hint Type                      | Examples                                   | Used to Specify                                                                 |
|--------------------------------|--------------------------------------------|---------------------------------------------------------------------------------|
| [Index](#Index)                | --splice-properties index=my\_index        | Which index to use or not use                                                   |
| [Join Order](#JoinOrder)       | --splice-properties joinOrder=fixed        | Which join order to use for two tables                                          |
| [Join Strategy](#JoinStrategy) | --splice-properties joinStrategy=sortmerge | How a join is processed (in conjunction with the Join Order hint)               |
| [Pinned Table](#Pinned)        | --splice-properties pin=true               | That you want the pinned (cached in memory) version of a table used in a query, |
| [Spark](#Spark)                | --splice-properties useSpark=true          | That you want a query to run (or not run) on Spark                              |

### Including Hints in Your Queries

Hints MUST ALWAYS be at the end of a line, meaning that you must always terminate hints with a newline character.
You cannot add the semicolon that terminates the command immediately after a hint; the semicolon must go on the next line, as shown in the examples in this topic.
Many of the examples in this section show usage of hints on the <span class="CodeFont">splice&gt;</span> command line. Follow the same rules when using hints programmatically.

Hints can be used in two locations: after a table identifier or after a <span class="CodeFont">FROM</span> clause. Some hint types can be use after a table identifier, and some can be used after a <span class="CodeFont">FROM</span> clause:

| Hint after a                                | Hint types   | Example                                           |
|---------------------------------------------|--------------|---------------------------------------------------|
| Table identifier                            | useSpark     
                                                             
                                               joinOrder     | ``` ExampleCell                                   
                                                              SELECT * FROM --SPLICE-PROPERTIES joinOrder=fixed  
                                                                 mytable1 e, mytable2 t                          
                                                                 WHERE e.id = t.parent_id;                       
                                                              ```                                                |
| A <span class="CodeFont">FROM</span> clause | joinStrategy 
                                                             
                                               index         | ``` ExampleCell                                   
                                                              SELECT * FROM                                      
                                                                 member_info m,                                  
                                                                 rewards r,                                      
                                                                 points p    --SPLICE-PROPERTIES index=ie_point  
                                                              WHERE...                                           
                                                              ```                                                |

This example shows proper placement of the hint and semicolon when the hint is at the end of statement:

``` Example
SELECT * FROM my_table --splice-properties index=my_index
;
```

If your command is broken into multiple lines, you still must add the hints at the end of the line, and you can add hints at the ends of multiple lines; for example:

``` Example
SELECT * FROM my_table_1 --splice-properties index=my_index
, my_table_2 --splice-properties index=my_index_2
WHERE my_table_1.id = my_table_2.parent_id;
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>In the above query, the first command line ends with the first index hint, because hints must always be the last thing on a command line. That's why the comma separating the table specifications appears at the beginning of the next line.

### []()Index Hints

Use <span class="ItalicFont">index hints</span> to tell the query interface how to use certain indexes for an operation.

To force the use of a particular index, you can specify the index name; for example:

``` Example
splice> SELECT * FROM my_table --splice-properties index=my_index
> ;
```

To tell the query interface to not use an index for an operation, specify the null index. For example:

``` Example
splice> SELECT * FROM my_table --splice-properties index=null
> ;
```

And to tell the query interface to use specific indexes on specific tables for an operation, you can add multiple hints. For example:

``` Example
splice> SELECT * FROM my_table_1   --splice-properties index=my_index
> , my_table_2                --splice-properties index=my_index_2
> WHERE my_table_1.id = my_table_2.parent_id;
```

#### Important Note About Placement of Index Hints

Each <span class="CodeFont">index</span> hint in a query <span class="BoldFont">MUST</span> be specified alongside the table containing the index, or an error will occur.

For example, if we have a table named <span class="CodeFont">points</span> with an index named <span class="CodeFont">ie\_point</span> and another table named `rewards` with an index named `ie_rewards`, then this hint works as expected:

``` Example
SELECT * FROM
   member_info m,
   rewards r,
   points p    --SPLICE-PROPERTIES index=ie_point
WHERE...
```

But the following hint will generate an error because <span class="CodeFont">ie\_rewards</span> is not an index on the points table.

``` Example
SELECT * FROM
   member_info m,
   rewards r,
   points p    --SPLICE-PROPERTIES index=ie_rewards
WHERE...
```

### []()JoinOrder Hints

Use <span class="CodeFont">JoinOrder</span> hints to tell the query interface in which order to join two tables. You can specify these values for a <span class="CodeFont">JoinOrder</span> hint:

-   Use <span class="CodeFont">joinOrder=FIXED</span> to tell the query optimizer to order the table join according to how where they are named in the <span class="CodeFont">FROM</span> clause.
-   Use <span class="CodeFont">joinOrder=UNFIXED</span> to specify that the query optimizer can rearrange the table order.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">joinOrder=UNFIXED</span> is the default, which means that you don't need to specify this hint to allow the optimizer to rearrange the table order.

Here are examples:

| Hint              | Example                                                                                                               |
|-------------------|-----------------------------------------------------------------------------------------------------------------------|
| joinOrder=FIXED   | <span class="AppCommand">splice&gt; </span><span class="Example">SELECT \* FROM --SPLICE-PROPERTIES joinOrder=fixed   
                     <span class="AppCommand">&gt; </span> mytable1 e, mytable2 t                                                           
                     <span class="AppCommand">&gt; </span>WHERE e.id = t.parent\_id;</span>                                                 |
| joinOrder=UNFIXED | <span class="AppCommand">splice&gt; </span><span class="Example">SELECT \* from --SPLICE-PROPERTIES joinOrder=unfixed 
                     <span class="AppCommand">&gt; </span>mytable1 e, mytable2 t WHERE e.id = t.parent\_id;</span>                          |

### []()JoinStrategy Hints

You can use a <span class="CodeFont">JoinStrategy</span> hint in conjunction with a <span class="CodeFont">joinOrder</span> hint to tell the query interface how to process a join. For example, this query specifies that the <span class="CodeFont">SORTMERGE</span> join strategy should be used:

``` Example
SELECT * FROM      --SPLICE-PROPERTIES joinOrder=fixed
   mytable1 e, mytable2 t --SPLICE-PROPERTIES joinStrategy=SORTMERGE
   WHERE e.id = t.parent_id;
```

And this uses a <span class="CodeFont">joinOrder</span> hint along with two <span class="CodeFont">joinStrategy</span> hints:

``` Example
SELECT *
  FROM --SPLICE-PROPERTIES joinOrder=fixed
  keyword k
  JOIN campaign c  --SPLICE-PROPERTIES joinStrategy=NESTEDLOOP
    ON k.campaignid = c.campaignid
  JOIN adgroup g  --SPLICE-PROPERTIES joinStrategy=NESTEDLOOP
    ON k.adgroupid = g.adgroupid
  WHERE adid LIKE '%us_gse%'
```

You can specify these join strategies:

| JoinStrategy Value                       | Strategy Description                                                                                                                                                                                                                        |
|------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="CodeFont">BROADCAST</span>  | Read the results of the Right Result Set (<span class="ItalicFont">RHS</span>) into memory, then for each row in the left result set (<span class="ItalicFont">LHS</span>), perform a local lookup to determine the right side of the join. 
                                                                                                                                                                                                                                                                                         
                                            <span class="CodeFont">BROADCAST</span> will only work on equijoin (<span class="CodeFont">=</span>) predicates that do not include a function call.                                                                                         |
| <span class="CodeFont">MERGE</span>      | Read the Right and Left result sets simultaneously in order and join them together as they are read.                                                                                                                                        
                                                                                                                                                                                                                                                                                         
                                            <span class="CodeFont">MERGE</span> joins require that both the left and right result sets be sorted according to the join keys. <span class="CodeFont">MERGE</span> requires an equijoin predicate that does not include a function call.   |
| <span class="CodeFont">NESTEDLOOP</span> | For each row on the left, fetch the values on the right that match the join.                                                                                                                                                                
                                                                                                                                                                                                                                                                                         
                                            <span class="CodeFont">NESTEDLOOP</span> is the only join that can work with any join predicate of any type; however this type of join is generally very slow.                                                                               |
| <span class="CodeFont">SORTMERGE</span>  | Re-sort both the left and right sides according to the join keys, then perform a <span class="CodeFont">MERGE</span> join on the results.                                                                                                   
                                                                                                                                                                                                                                                                                         
                                            <span class="CodeFont">SORTMERGE</span> requires an equijoin predicate with no function calls.                                                                                                                                               |

### []()Pinned Table Hint

You can use the <span class="CodeFont">pin</span> hint to specify to specify that you want a query to run against a pinned version of a table.

``` Example
splice> PIN TABLE myTable;
splice> SELECT COUNT(*) FROM my_table --splice-properties pin=true
> ;
```

You can read more about pinning tables in the <span class="CodeFont">[PIN TABLE](../../SQLReference/Statements/PinTable.html)</span> statement topic in our <span class="ItalicFont">SQL Reference Guide</span>.

### []()Spark Hints

You can use the <span class="CodeFont">useSpark</span> hint to specify to the optimizer that you want a query to run on (or not on) Spark. The Splice Machine query optimizer automatically determines whether to run a query through our Spark engine or our HBase engine, based on the type of query; you can override this by using a hint:

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The Splice Machine optimizer uses its estimated cost for a query to decide whether to use spark. If your statistics are out of date, the optimizer may end up choosing the wrong engine for the query.

``` Example
splice> SELECT COUNT(*) FROM my_table --splice-properties useSpark=true
> ;
```

You can also specify that you want the query to run on HBase and not on Spark. For example:

``` Example
splice> SELECT COUNT(*) FROM your_table --splice-properties useSpark=false
> ;
```

You can read more about the Splice Spark and HBase engines in the [Splice Machine Architectural Overview](../../../OnPremise/GettingStarted/ArchitectureOvervew.html) topic in our <span class="ItalicFont">Getting Started Guide</span>.

 


