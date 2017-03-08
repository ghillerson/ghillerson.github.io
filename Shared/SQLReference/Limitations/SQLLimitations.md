[Open topic with navigation](../../../index.html#Shared/SQLReference/Limitations/SQLLimitations.html)

<a href="" id="SQLReference.SQLReservedWords"></a>[]()SQL Limitations
=====================================================================

This topic specifies limitations for various values in Splice Machine SQL:

-   [Database Value Limitations](#Database)
-   [Date, Time, and TimeStamp Limitations](#DATE)
-   [Identifier Length Limitations](#Identifier)
-   [Numeric Limitations](#Numeric)
-   [String Limitations](#String)
-   [XML Limitations](#XML)

[]()Database Value Limitations
------------------------------

The following table lists limitations on various database values in Splice Machine.

| Value                                                                                                      | Limit                                                                                                     |
|------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Maximum columns in a table                                                                                 | <span class="LimitationsMaxColumnsInTable">100000</span>                                                  |
| Maximum columns in a view                                                                                  | <span class="LimitationsMaxColumnsInView">5000</span>                                                     |
| Maximum number of parameters in a stored procedure                                                         | <span class="LimitationsMaxParamsInStoredProc">90</span>                                                  |
| Maximum indexes on a table                                                                                 | <span class="LimitationsMaxIndexesOnTable">32767</span><span class="bodyFont"> or storage capacity</span> |
| Maximum tables referenced in an SQL statement or a view                                                    | Storage capacity                                                                                          |
| Maximum elements in a select list                                                                          | <span class="LimitationsMaxElementsSelect">1012</span>                                                    |
| Maximum predicates in a <span class="CodeFont">WHERE</span> or <span class="CodeFont">HAVING</span> clause | Storage capacity                                                                                          |
| Maximum number of columns in a <span class="CodeFont">GROUP BY</span> clause                               | <span class="LimitationsMaxElementsGroupBy">32677</span>                                                  |
| Maximum number of columns in an <span class="CodeFont">ORDER BY</span> clause                              | <span class="LimitationsMaxElementsOrderBy">1012</span>                                                   |
| Maximum number of prepared statements                                                                      | Storage capacity                                                                                          |
| Maximum declared cursors in a program                                                                      | Storage capacity                                                                                          |
| Maximum number of cursors opened at one time                                                               | Storage capacity                                                                                          |
| Maximum number of constraints on a table                                                                   | Storage capacity                                                                                          |
| Maximum level of subquery nesting                                                                          | Storage capacity                                                                                          |
| Maximum number of subqueries in a single statement                                                         | Storage capacity                                                                                          |
| Maximum number of rows changed in a unit of work                                                           | Storage capacity                                                                                          |
| Maximum constants in a statement                                                                           | Storage capacity                                                                                          |
| Maximum depth of cascaded triggers                                                                         | <span class="LimitationsMaxTriggerRecursion">16</span>                                                    |

[]()Date, Time, and TimeStamp Limitations
-----------------------------------------

The following table lists limitations on date, time, and timestamp values in Splice Machine.

| Value                                                  | Limit                      |
|--------------------------------------------------------|----------------------------|
| Smallest <span class="CodeFont">DATE</span> value      | 0001-01-01                 |
| Largest <span class="CodeFont">DATE</span> value       | 9999-12-31                 |
| Smallest <span class="CodeFont">TIME</span> value      | 00:00:00                   |
| Largest <span class="CodeFont">TIME</span> value       | 24:00:00                   |
| Smallest <span class="CodeFont">TIMESTAMP</span> value | 1677-09-21-00.12.44.000000 |
| Largest <span class="CodeFont">TIMESTAMP</span> value  | 2262-04-11-23.47.16.999999 |

[]()Identifier Length Limitations
---------------------------------

The following table lists limitations on identifier lengths in Splice Machine.

| Identifier                                               | Maximum Number of Characters Allowed |
|----------------------------------------------------------|--------------------------------------|
| Constraint name                                          | 128                                  |
| Correlation name                                         | 128                                  |
| Cursor name                                              | 128                                  |
| Data source column name                                  | 128                                  |
| Data source index name                                   | 128                                  |
| Data source name                                         | 128                                  |
| Savepoint name                                           | 128                                  |
| Schema name                                              | 128                                  |
| Unqualified column name                                  | 128                                  |
| Unqualified function name                                | 128                                  |
| Unqualified index name                                   | 128                                  |
| Unqualified procedure name                               | 128                                  |
| Parameter name                                           | 128                                  |
| Unqualified trigger name                                 | 128                                  |
| Unqualified table name, view name, stored procedure name | 128                                  |

[]()Numeric Limitations
-----------------------

The following lists limitations on the numeric values in Splice Machine.

| Value                                                  | Limit                      |
|--------------------------------------------------------|----------------------------|
| Smallest <span class="CodeFont">INTEGER</span>         | -2,147,483,648             |
| Largest <span class="CodeFont">INTEGER</span>          | 2,147,483,647              |
| Smallest <span class="CodeFont">BIGINT</span>          | -9,223,372,036,854,775,808 |
| Largest <span class="CodeFont">BIGINT</span>           | 9,223,372,036,854,775,807  |
| Smallest <span class="CodeFont">SMALLINT</span>        | -32,768                    |
| Largest <span class="CodeFont">SMALLINT</span>         | 32,767                     |
| Largest decimal precision                              | 31                         |
| Smallest <span class="CodeFont">DOUBLE</span>          | -1.79769E+308              |
| Largest <span class="CodeFont">DOUBLE</span>           | 1.79769E+308               |
| Smallest positive <span class="CodeFont">DOUBLE</span> | 2.225E-307                 |
| Largest negative <span class="CodeFont">DOUBLE</span>  | -2.225E-307                |
| Smallest <span class="CodeFont">REAL</span>            | -3.402E+38                 |
| Largest <span class="CodeFont">REAL</span>             | 3.402E+38                  |
| Smallest positive <span class="CodeFont">REAL</span>   | 1.175E-37                  |
| Largest negative <span class="CodeFont">REAL</span>    | -1.175E-37                 |

[]()String Limitations
----------------------

The following table lists limitations on string values in Splice Machine.

| Value                                                         | Maximum Limit                                          |
|---------------------------------------------------------------|--------------------------------------------------------|
| Length of <span class="CodeFont">CHAR</span>                  | <span class="CodeFont">254</span> characters           |
| Length of <span class="CodeFont">VARCHAR</span>               | <span class="CodeFont">32,672</span> characters        |
| Length of <span class="CodeFont">LONG VARCHAR</span>          | <span class="CodeFont">32,670</span> characters        |
| Length of <span class="CodeFont">CLOB</span>                  | <span class="CodeFont">2,147,483,647</span> characters |
| Length of <span class="CodeFont">BLOB</span>                  | <span class="CodeFont">2,147,483,647</span> characters |
| Length of character constant                                  | <span class="CodeFont">32,672</span>                   |
| Length of concatenated character string                       | <span class="CodeFont">2,147,483,647</span>            |
| Length of concatenated binary string                          | <span class="CodeFont">2,147,483,647</span>            |
| Number of hex constant digits                                 | <span class="CodeFont">16,336</span>                   |
| Length of <span class="CodeFont">DOUBLE</span> value constant | <span class="CodeFont">30</span> characters            |

 


