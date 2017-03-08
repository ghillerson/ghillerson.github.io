[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateProcedure.html)

<a href="" id="Statements.CreateFunction"></a>[]()CREATE PROCEDURE
==================================================================

The <span class="CodeFont">CREATE PROCEDURE</span> statement allows you to create Java procedures, which you can then call using the <span class="CodeFont">CALL PROCEDURE</span> statement.

For details on how Splice Machine matches procedures to Java methods, see [Argument matching](../ArgMatching/ArgumentMatching.html).

Syntax

``` FcnSyntax
CREATE PROCEDURE procedureName (
    [ procedureParameter 
    [, procedureParameter] ] * 
    )
     [ ProcedureElement ] *
```

procedureName

``` FcnSyntax
[ schemaName. ] SQL Identifier
```

If <span class="CodeFont">schemaName</span> is not provided, then the current schema is the default schema. If a qualified procedure name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

procedureParameter

``` FcnSyntax
[ { IN | OUT | INOUT } ] [ parameterName ] DataType
```

<span class="CodeFont">parameterName</span> is an identifier that must be unique within the procedure's parameter names.

By default, parameters are <span class="CodeFont">IN</span> parameters unless you specify otherwise.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Data-types such as <span class="CodeFont">BLOB, CLOB, LONG VARCHAR</span> are not allowed as parameters in a <span class="CodeFont">CREATE PROCEDURE</span> statement.
Also: At this time, Splice Machine will return only one <span class="CodeFont">ResultSet</span> from a stored procedure.

procedureElement

See the description of [procedure Elements](#FunctionElements) in the next section.

[]()Procedure Elements

``` FcnSyntax
 {
    LANGUAGE { JAVA }
  | DeterministicCharacteristic
  | EXTERNAL NAME javaMethodName
  | PARAMETER STYLE parameterStyle
  | sqlStatementType
}
```

The procedure elements may appear in any order, but each type of element can only appear once. These procedure elements are required:

-    <span class="ItalicFont">LANGUAGE</span>
-   <span class="ItalicFont">EXTERNAL NAME</span>
-   <span class="ItalicFont">PARAMETER STYLE</span>

LANGUAGE

Only <span class="CodeFont">JAVA</span> is accepted at this time. Splice Machine will call the procedure as a public static method in a Java class.

DeterministicCharacteristic

``` FcnSyntax
DETERMINISTIC | NOT DETERMINISTIC
```

The default value is <span class="CodeFont">NOT DETERMINISTIC</span>.

Specifying <span class="CodeFont">DETERMINISTIC</span> indicates that the procedure always returns the same result, given the same input values. This allows Splice Machine to call the procedure with greater efficiency; however, specifying this for a procedure that is actually non-deterministic will have the opposite effect -- efficiency of calls to the procedure will be reduced.

javaMethodName

``` FcnSyntax
class_name.method_name
```

This is the name of the Java method to call when this procedure executes.

parameterStyle

``` FcnSyntax
JAVA
```

Stored procedures use a parameter-passing convention is used that conforms to the Java language and SQL Routines specification. <span class="CodeFont">INOUT</span> and <span class="CodeFont">OUT</span> parameters are passed as single entry arrays to facilitate returning values. Result sets can be returned through additional parameters to the Java method of type <span class="CodeFont">java.sql.ResultSet\[\]</span> that are passed single entry arrays.

Splice Machine does not support long column types such as <span class="CodeFont">LONG VARCHAR</span>or <span class="CodeFont">BLOB</span>; an error will occur if you try to use one of these long column types.

sqlStatementType

CONTAINS SQL

Indicates that SQL statements that neither read nor modify SQL data can be executed by the procedure.

NO SQL

Indicates that the procedure cannot execute any SQL statements

READS SQL DATA

Indicates that some SQL statements that do not modify SQL data can be included in the procedure. This is the default value.

MODIFIES SQL DATA

Indicates that the procedure can execute any SQL statement.

Example

The following example depends on a fictionalized java class. For functional examples of using <span class="CodeFont">CREATE PROCEDURE</span>, please see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section of our <span class="ItalicFont">Developer's Guide</span>.

``` Example
splice> CREATE PROCEDURE SALES.TOTAL_REVENUE (
    IN S_MONTH INTEGER,
    IN S_YEAR INTEGER, OUT TOTAL DECIMAL(10,2))
    PARAMETER STYLE JAVA 
    READS SQL DATA LANGUAGE
    JAVA EXTERNAL NAME 'com.example.sales.calculateRevenueByMonth';
0 rows inserted/updated/deleted
```

See Also

-   [Argument matching](../ArgMatching/ArgumentMatching.html)
-   [<span class="CodeFont">CREATE\_FUNCTION</span>](CreateFunction.html) statement
-   [<span class="CodeFont">CURRENT\_USER</span>](../BuiltInFcns/CurrentUser.html) function
-   [Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   [SQL Identifier](../Identifiers/Intro.Identifiers.html)
-   [<span class="CodeFont">SESSION\_USER</span>](../BuiltInFcns/SessionUser.html) function
-   [<span class="CodeFont">USER</span>](../BuiltInFcns/User.html) function

 


