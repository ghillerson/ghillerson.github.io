[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/GenerationClause.html)

<a href="" id="Statements.GenerationClause"></a>[]()generation-clause
=====================================================================

Syntax

``` FcnSyntax
GENERATED ALWAYS AS ( value-expression )
```

value-expression

An <span class="ItalicFont">[Expression](../Expressions/AboutExpressions.html)</span> that resolves to a single value, with some limitations:

-   The <span class="ItalicFont">generation-clause</span> may reference other non-generated columns in the table, but it must not reference any generated column. The <span class="ItalicFont">generation-clause</span> must not reference a column in another table.
-   The <span class="ItalicFont">generation-clause</span> must not include subqueries.
-   The <span class="ItalicFont">generation-clause</span> may invoke user-coded functions, if the functions meet the requirements in the [User Function Restrictions](#UserFunctions) section below.

[]()User Function Restrictions

The <span class="ItalicFont">generation-clause</span> may invoke user-coded functions, if the functions meet the following requirements:

-   The functions must not read or write SQL data.
-   The functions must have been declared <span class="CodeFont">DETERMINISTIC</span>.
-   The functions must not invoke any of the following possibly non-deterministic system functions:
    -   [CURRENT\_DATE](../BuiltInFcns/CurrentDate.html)
    -   [CURRENT\_TIME](../BuiltInFcns/CurrentTime.html)
    -   [CURRENT\_TIMESTAMP](../BuiltInFcns/CurrentTimestamp.html)
    -   [CURRENT\_USER](../BuiltInFcns/CurrentUser.html)
    -   [CURRENT\_ROLE](../BuiltInFcns/CurrentRole.html)
    -   [CURRENT SCHEMA](../BuiltInFcns/CurrentSchema.html)
    -   [SESSION\_USER](../BuiltInFcns/SessionUser.html)

Example

``` Example
CREATE TABLE employee(
  employeeID           int,   
  name                 varchar( 50 ),
  caseInsensitiveName  GENERATED ALWAYS AS( UPPER( name ) )
  );

CREATE INDEX caseInsensitiveEmployeeName
  ON employee( caseInsensitiveName );
```

 


