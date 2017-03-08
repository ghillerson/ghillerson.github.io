[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropFunction.html)

<a href="" id="Statements.DropFunction"></a>[]()DROP FUNCTION
=============================================================

The <span class="CodeFont">DROP FUNCTION</span> statement drops a function from your database. Functions are added to the database with the <span class="CodeFont">[CREATE FUNCTION](CreateFunction.html)</span> statement.

Syntax

``` FcnSyntax
DROP FUNCTION function-name
```

function-Name

The name of the function that you want to drop from your database.

Usage

Use this statement to drop a function from your database. It is valid only if there is exactly one function instance with the <span class="ItalicFont">function-name</span> in the schema. The specified function can have any number of parameters defined for it.

An error will occur in any of the following circumstances:

-   If no function with the indicated name exists in the named or implied schema (the error is SQLSTATE 42704)
-   If there is more than one specific instance of the function in the named or implied schema
-   If you try to drop a user-defined function that is invoked in the <span class="ItalicFont">[generation-clause](GenerationClause.html)</span> of a generated column
-   If you try to drop a user-defined function that is invoked in a view

Example

``` Example
splice> DROP FUNCTION TO_DEGREES;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CREATE FUNCTION</span>](CreateProcedure.html) statement

 


