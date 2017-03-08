[Open topic with navigation](../../../index.html#Shared/Developers/FcnsAndProcs/Intro.FcnsAndProcs.html)

Using Functions and Stored Procedures
=====================================

This topic provides an overview of writing and using functions and stored procedures in Splice Machine.

About User-Defined Functions
----------------------------

You can create user-defined database functions that can be evaluated in SQL statements; these functions can be invoked where most other built-in functions are allowed, including within SQL expressions and <span class="CodeFont">SELECT</span> statement. Functions must be deterministic, and cannot be used to make changes to the database.

You can create two kinds of functions:

-   Scalar functions, which always return a single value (or <span class="CodeFont">NULL</span>),
-   Table functions, which return a table.

When you invoke a function within a <span class="CodeFont">SELECT</span> statement, it is applied to each retrieved row. For example:

``` Example
SELECT ID, Salary, MyAdjustSalaryFcn(Salary) 
FROM SPLICEBBALL.Salaries;
```

This <span class="CodeFont">SELECT</span> will execute the <span class="CodeFont">MyAdjustSalaryFcn</span> to the <span class="CodeFont">Salary</span> value for each player in the table.

About Stored Procedures
-----------------------

You can group a set of SQL commands together with variable and logic into a stored procedure, which is a subroutine that is stored in your database's data dictionary. Unlike user-defined functions, a stored procedure is not an expression and can only be invoked using the <span class="CodeFont">CALL</span> statement. Stored procedures allow you to modify the database and return <span class="CodeFont">Result Sets</span> or nothing at all.

Stored procedures can be used for situations where a complex set of SQL statements are required to process something, and that process is used by various applications; creating a stored procedure increases performance efficiency. They are typically used for:

-   checking business rules and validating data before performing actions
-   performing significant processing of data with the inputs to the procedure

[]()Comparison of Functions and Stored Procedures
-------------------------------------------------

Here's a comparison of Splice Machine functions and stored procedures:

| Database Function                                                                                                                                                           | Stored Procedure                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A Splice Machine database function:                                                                                                                                         
                                                                                                                                                                              
 -   must be written as a public static method in a Java public class                                                                                                         
 -   is executed in exactly the same manner as are public static methods in Java                                                                                              
 -   can have multiple input parameters                                                                                                                                       
 -   always returns a single value (which can be null)                                                                                                                        
 -   cannot modify data in the database                                                                                                                                       | Splice Machine stored procedures can:                                                                                                                                         
                                                                                                                                                                                                                                                                                                                                                              
                                                                                                                                                                               -   return result sets or return nothing at all                                                                                                                                
                                                                                                                                                                               -   issue <span class="CodeFont">update</span>, <span class="CodeFont">insert</span>, and <span class="CodeFont">delete</span> statements                                      
                                                                                                                                                                               -   perform DDL statements such as <span class="CodeFont">create</span> and <span class="CodeFont">drop</span>                                                                 
                                                                                                                                                                               -   consolidate and centralize code                                                                                                                                            
                                                                                                                                                                               -   reduce network traffic and increase execution speed                                                                                                                        |
| Can be used in <span class="CodeFont">SELECT</span> statements.                                                                                                             | Cannot be used in in <span class="CodeFont">SELECT</span> statements.                                                                                                         
                                                                                                                                                                                                                                                                                                                                                              
                                                                                                                                                                               Must be invoked using a <span class="CodeFont">CALL</span> statement.                                                                                                          |
| Create with the <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html)</span> statement, which is described in our SQL Reference book. 
                                                                                                                                                                              
 You can find an example in the [Function and Stored Procedure Examples](ProcAndFcnExamples.html) topic in this section.                                                      | Create with the <span class="CodeFont">[CREATE PROCEDURE](../../SQLReference/Statements/CreateProcedure.html)</span> statement, which is described in our SQL Reference book. 
                                                                                                                                                                                                                                                                                                                                                              
                                                                                                                                                                               You can find an example in the [Function and Stored Procedure Examples](ProcAndFcnExamples.html) topic in this section.                                                        |

Operations in Which You Can Use Functions and Stored Procedures
---------------------------------------------------------------

The following table provides a list of the differences between functions and stored procedures with regard to when and where they can be used:

| Operation                                                                                      | Functions | Stored Procedures                                                                                                   |
|------------------------------------------------------------------------------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| <span class="ItalicFont">Execute in an SQL Statement</span>                                    | Yes       | No                                                                                                                  |
| <span class="ItalicFont">Execute in a Trigger</span>                                           | Yes       | Triggers that execute before an operation (<span class="ItalicFont">before triggers</span>) cannot modify SQL data. |
| <span class="ItalicFont">Process <span class="CodeFont">OUT / INOUT</span> Parameters</span>   | No        | Yes                                                                                                                 |
| <span class="ItalicFont">Return <span class="CodeFont">Resultset(s)</span></span>              | No        | Yes                                                                                                                 |
| <span class="ItalicFont">Execute SQL <span class="CodeFont">Select</span></span>               | Yes       | Yes                                                                                                                 |
| <span class="ItalicFont">Execute SQL <span class="CodeFont">Update/Insert/Delete</span></span> | No        | Yes                                                                                                                 |
| <span class="ItalicFont">Execute DDL (<span class="CodeFont">Create/Drop</span>)</span>        | No        | Yes                                                                                                                 |

Viewing Functions and Stored Procedures
---------------------------------------

You can use the [show command](../../CmdLineReference/ShowCmds.html) in the <span class="AppCommand">splice&gt;</span> command line interface to display the functions and stored procedures available in your database:

| Command                                                                    | Output                                                                                         |
|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| <span class="AppCommand">splice&gt; show functions;</span>                 | All functions defined in your database                                                         |
| <span class="AppCommand">splice&gt; show functions in SYSCS\_UTIL;</span>  | All functions in the <span class="CodeFont">SYSCS\_UTIL</span> schema in your database         |
| <span class="AppCommand">splice&gt; show procedures;</span>                | All stored procedures defined in your database                                                 |
| <span class="AppCommand">splice&gt; show procedures in SYSCS\_UTIL;</span> | All stored procedures in the <span class="CodeFont">SYSCS\_UTIL</span> schema in your database |

Writing and Deploying Functions and Stored Procedures
-----------------------------------------------------

The remainder of this section presents information about and examples of writing functions and stored procedures for use with Splice Machine, in these topics:

-   [Writing Functions and Stored Procedures](WritingProcsAndFcns.html) shows you the steps required to write functions stored procedures and add them to your Splice Machine database.
-   [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) tells you how to store new JAR files, replace JAR files, and remove JAR files in your Splice Machine database.
-   [Examples of Splice Machine Functions and Stored Procedures](ProcAndFcnExamples.html) provides you with examples of functions and stored procedures.

See Also
--------

-   <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CREATE PROCEDURE](../../SQLReference/Statements/CreateProcedure.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>

 


