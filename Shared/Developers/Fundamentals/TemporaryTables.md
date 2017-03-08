[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/TemporaryTables.html)

Using Temporary Database Tables
===============================

This topic describes how to use temporary tables with Splice Machine.

About Temporary Tables
----------------------

You can use temporary tables when you want to temporarily save a result set for further processing. One common case for doing so is when you've constructed a result set by running multiple queries. You can also use temporary tables when performing complex queries that require extensive operations such as repeated multiple joins or sub-queries. Storing intermediate results in a temporary table can reduce overall processing time.

An example of using a temporary table to store intermediate results is a web-based application for travel reservations that allows customers to create several alternative itineraries, compare them, and then select one for purchase. Such an app could store each itinerary in a row in a temporary table, using table updates whenever the itinerary changes. When the customer decides upon a final itinerary, that temporary row is copied into a persistent table. And when the customer session ends, the temporary table is automatically dropped.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Creating and operating with temporary tables does consume resources, and can affect performance of your queries.

Creating Temporary Tables
-------------------------

Splice Machine provides two statements you can use to create a temporary table; we provide multiple ways to create temporary tables to maintain compatibility with third party Business Intelligence tools.

<span class="autonumber"><span class="noteAutoNum">RESTRICTION:  </span></span>Splice Machine does not currently support creating temporary tables stored as external tables.

Each of these statements creates the same kind of temporary table, using different syntax

| Statement                                                                                                                 | Syntax                                               |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| <span class="CodeFont">[CREATE TEMPORARY TABLE](../../SQLReference/Statements/CreateTempTable.html)</span>                | ``` FcnSyntaxCell                                    
                                                                                                                             CREATE [LOCAL | GLOBAL] TEMPORARY TABLE table-Name {  
                                                                                                                                   ( {column-definition | Table-level constraint}  
                                                                                                                                      [ , {column-definition} ] * )                
                                                                                                                                   ( column-name [ , column-name ] * )             
                                                                                                                               }                                                   
                                                                                                                               [NOLOGGING | ON COMMIT PRESERVE ROWS];              
                                                                                                                             ```                                                   |
| <span class="CodeFont">[DECLARE GLOBAL TEMPORARY TABLE](../../SQLReference/Statements/DeclareGlobalTempTable.html)</span> | ``` FcnSyntaxCell                                    
                                                                                                                             DECLARE GLOBAL TEMPORARY TABLE table-Name             
                                                                                                                                { column-definition[ , column-definition] * }      
                                                                                                                                 [ON COMMIT PRESERVE ROWS ]                        
                                                                                                                                 [NOT LOGGED];                                     
                                                                                                                             ```                                                   |

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine generates a warning if you attempt to specify any other modifiers other than the <span class="CodeFont">NOLOGGING</span>, <span class="CodeFont">NOT LOGGED</span>, and <span class="CodeFont">ON COMMIT PRESERVE ROWS</span> modifiers shown above.

Restrictions on Temporary Tables
--------------------------------

You can use temporary tables just like you do permanently defined database tables, with several important exceptions and restrictions that are noted in this section, including these:

-   [Operational Limitations](#Operatio)
-   [Table Persistence](#Table)

### []()Operational Limitations

Temporary tables have the following operational limitations; they:

-   exist only while a user session is alive
-   are visible in system tables, but are otherwise not visible to other sessions or transactions
-   cannot be altered using the <span class="CodeFont">[ALTER TABLE](../../SQLReference/Statements/AlterTable.html)</span>, <span class="CodeFont">[RENAME TABLE](../../SQLReference/Statements/RenameTable.html)</span>, or <span class="CodeFont">[RENAME COLUMN](../../SQLReference/Statements/RenameColumn.html)</span> statements
-   do not get backed up
-   cannot be used as data providers to views
-   cannot be referenced by foreign keys in other tables
-   are not displayed by the [show](../../CmdLineReference/ShowCmds.html) command

Also note that temporary tables persist across transactions in a session and are automatically dropped when a session terminates.

### []()Table Persistence

Here are two important notes about temporary table persistence. Temporary tables:

-   persist across transactions in a session
-   are automatically dropped when a session terminates or expires
-   can also be dropped with the <span class="CodeFont">[DROP TABLE](../../SQLReference/Statements/DropTable.html)</span> statement

Example
-------

``` Example
create local temporary table temp_num_dt (
   smallint_col smallint not null,   
   int_col int,
   primary key(smallint_col)) on commit preserve rows;
insert into temp_num_dt values (1,1);
insert into temp_num_dt values (3,2),(4,2),(5,null),(6,4),(7,8);
insert into temp_num_dt values (13,2),(14,2),(15,null),(16,null),(17,8);
select * from temp_num_dt;
```

See Also
--------

-   <span class="CodeFont">[ALTER TABLE](../../SQLReference/Statements/AlterTable.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CREATE TEMPORARY TABLE](../../SQLReference/Statements/CreateTempTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[DECLARE GLOBAL TEMPORARY TABLE](../../SQLReference/Statements/DeclareGlobalTempTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[DROP TABLE](../../SQLReference/Statements/DropTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[RENAME COLUMN](../../SQLReference/Statements/RenameColumn.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[RENAME TABLE](../../SQLReference/Statements/RenameTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SHOW](../../CmdLineReference/ShowCmds.html)</span> command

 


