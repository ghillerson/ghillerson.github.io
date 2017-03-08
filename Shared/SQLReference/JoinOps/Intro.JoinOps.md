[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/Intro.JoinOps.html)

[]()Join Operations
===================

This section contains the reference documentation for the Splice Machine SQL Join Operations, in the following topics:

| Topic                                    | Description                                                                                                                                                                                   |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [About Join Operations](AboutJoins.html) | Overview of joins.                                                                                                                                                                            |
| [CROSS JOIN](CrossJoin.html)             | Produces the Cartesian product of two tables: it produces rows that combine each row from the first table with each row from the second table.                                                |
| [INNER JOIN](InnerJoin.html)             | Selects all rows from both tables as long as there is a match between the columns in both tables.                                                                                             |
| [LEFT OUTER JOIN](LeftOuterJoin.html)    | Returns all rows from the left table (table1), with the matching rows in the right table (table2). The result is <span class="CodeFont">NULL</span> in the right side when there is no match. |
| [NATURAL JOIN](NaturalJoin.html)         | Creates an implicit join clause for you based on the common columns (those with the same name in both tables) in the two tables being joined.                                                 |
| [RIGHT OUTER JOIN](RightOuterJoin.html)  | Returns all rows from the right table (table2), with the matching rows in the left table (table1). The result is <span class="CodeFont">NULL</span> in the left side when there is no match.  |

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

 


