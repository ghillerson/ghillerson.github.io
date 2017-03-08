[Open topic with navigation](../../../index.html#Shared/Developers/TuningAndDebugging/ExplainPlan.html)

About Explain Plan
==================

You can use the <span class="CodeFont">explain</span> command to display what the execution plan will be for a statement without executing the statement. This topic presents and describes several examples.

Using Explain Plan to See the Execution Plan for a Statement
------------------------------------------------------------

To display the execution plan for a statement without actually executing the statement, use the <span class="AppCommand">explain</span> command on the statement:

``` AppCommand
splice> explain Statement;
```

Statement

An SQL statement.

### Explain Plan and DDL Statements

SQL Data Definition Language (DDL) statements have no known cost, and thus do not require optimization. Because of this, the <span class="CodeFont">explain</span> command does not work with DDL statements; attempting to <span class="CodeFont">explain</span> a DDL statement such as <span class="CodeFont">CREATE TABLE</span> will generate a syntax error. You <span class="BoldFont">cannot</span> use <span class="CodeFont">explain</span> with any of the following SQL statements:

-   ALTER
-   CREATE ... <span class="bodyFont">(any statement that starts with <span class="CodeFont">CREATE</span>)</span>
-   DROP ... <span class="bodyFont">(any statement that starts with <span class="CodeFont">DROP</span>)</span>
-   GRANT
-   RENAME ... <span class="bodyFont">(any statement that starts with <span class="CodeFont">RENAME</span>)</span>
-   REVOKE
-   TRUNCATE TABLE

Explain Plan Output
-------------------

When you run the <span class="CodeFont">explain</span> command, it displays output in a tree-structured format:

-   The first row in the output summarizes the plan
-   Each row in the output represents a node in the tree.
-   For join nodes, the right side of the join is displayed first, followed by the left side.
-   Child node rows are indented and prefixed with '<span class="CodeFont">-&gt;</span>'.

The first node in the plan output contains these fields:

| Field                                       | Description                                                                                            |
|---------------------------------------------|--------------------------------------------------------------------------------------------------------|
| n=<span class="ItalicFont">number</span>    | The number of nodes.                                                                                   |
| rows=<span class="ItalicFont">number</span> | The number of output rows.                                                                             |
| updateMode=\[mode\]                         | The update mode of the statement.                                                                      |
| engine=\[engineType\]                       | engineType=<span class="CodeFont">Spark</span> means this query will be executed by our OLAP engine.   
                                                                                                                                                       
                                               engineType=<span class="CodeFont">control</span> means this query will be executed by our OLTP engine.  |

Each node row in the output contains the following fields:

| Field                                                      | Description                                                                                                                                                                     |
|------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \[<span class="ItalicFont">node label</span>\]             | The name of the node                                                                                                                                                            |
| n=<span class="ItalicFont">number</span>                   | The result set number.                                                                                                                                                          
                                                                                                                                                                                                                                               
                                                              This is primarily used internally, and can also be used to determine the relative ordering of optimization.                                                                      |
| totalCost=<span class="ItalicFont">number</span>           | The total cost to perform this operation.                                                                                                                                       
                                                                                                                                                                                                                                               
                                                              This is computed <span class="ItalicFont">as if the operation is at the top of the operation tree</span>.                                                                        |
| processingCost=<span class="ItalicFont">number</span>      | The cost to process all data in this node.                                                                                                                                      
                                                                                                                                                                                                                                               
                                                              Processing includes everything except for reading the final results over the network.                                                                                            |
| transferCost=<span class="ItalicFont">number</span>        | The cost to send the final results over the network to the control node.                                                                                                        |
| outputRows=<span class="ItalicFont">number</span>          | The total number of rows that are output.                                                                                                                                       |
| outputHeapSize=<span class="ItalicFont">number unit</span> | The total size of the output result set, and the unit in which that size is expressed, which is one of:                                                                         
                                                                                                                                                                                                                                               
                                                              -   B                                                                                                                                                                            
                                                              -   KB                                                                                                                                                                           
                                                              -   MB                                                                                                                                                                           
                                                              -   GB                                                                                                                                                                           
                                                              -   TB                                                                                                                                                                           |
| partitions==<span class="ItalicFont">number</span>         | The number of partitions involved.                                                                                                                                              
                                                                                                                                                                                                                                               
                                                              <span class="ItalicFont">Partition</span> is currently equivalent to <span class="ItalicFont">Region</span>; however, this will not necessarily remain true in future releases.  |

For example:

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

The next topic, [Explain Plan Examples](ExplainPlanExamples.html), contains a number of examples, annotated with notes to help you understand the output of each.

See Also
--------

-   [Explain Plan Examples](ExplainPlanExamples.html)

 


