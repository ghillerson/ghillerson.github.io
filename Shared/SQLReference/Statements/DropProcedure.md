[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropProcedure.html)

<a href="" id="Statements.DropProcedure"></a>[]()DROP PROCEDURE
===============================================================

The <span class="CodeFont">DROP PROCEDURE</span> statement drops a procedure from your database. Procedures are added to the database with the <span class="CodeFont">[CREATE PROCEDURE](CreateProcedure.html)</span> statement.

Syntax

``` FcnSyntax
DROP PROCEDURE procedure-name
```

procedure-Name

The name of the procedure that you want to drop from your database.

Usage

Use this statement to drop a statement from your database. It is valid only if there is exactly one procedure instance with the <span class="ItalicFont">procedure-name</span> in the schema. The specified procedure can have any number of parameters defined for it.

An error will occur in any of the following circumstances:

-   If no procedure with the indicated name exists in the named or implied schema (the error is SQLSTATE 42704)
-   If there is more than one specific instance of the procedure in the named or implied schema
-   If you try to drop a user-defined procedure that is invoked in the <span class="ItalicFont">[generation-clause](GenerationClause.html)</span> of a generated column
-   If you try to drop a user-defined procedure that is invoked in a view

Example

``` Example
splice> DROP PROCEDURE SALES.TOTAL_REVENUE;
0 rows inserted/updated/deleted
```

See Also

-   [Argument matching](../ArgMatching/ArgumentMatching.html)
-   [<span class="CodeFont">CREATE\_PROCEDURE</span>](CreateProcedure.html) statement
-   [<span class="CodeFont">CURRENT\_USER</span>](../BuiltInFcns/CurrentUser.html) function
-   [Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   [SQL Identifier](../Identifiers/Intro.Identifiers.html)
-   [<span class="CodeFont">SESSION\_USER</span>](../BuiltInFcns/SessionUser.html) function
-   [<span class="CodeFont">USER</span>](../BuiltInFcns/User.html) function

 


