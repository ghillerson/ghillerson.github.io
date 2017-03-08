[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateFunction.html)

<a href="" id="Statements.CreateFunction"></a>[]()CREATE FUNCTION
=================================================================

The <span class="CodeFont">CREATE FUNCTION</span> statement allows you to create Java functions, which you can then use in expressions.

For details on how Splice Machine matches functions to Java methods, see [Argument matching](../ArgMatching/ArgumentMatching.html).

Syntax

``` FcnSyntax
CREATE FUNCTION functionName (
    [ functionParameter 
    [, functionParameter] ] * 
    )
    RETURNS returnDataType [ functionElement ] *
```

functionName

``` FcnSyntax
[ schemaName. ] SQL Identifier
```

If <span class="CodeFont">schemaName</span> is not provided, then the current schema is the default schema. If a qualified procedure name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

functionParameter

``` FcnSyntax
[ parameterName ] DataType
```

<span class="CodeFont">parameterName</span> is an identifier that must be unique within the function's parameter names.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Data-types such as <span class="CodeFont">BLOB, CLOB, LONG VARCHAR</span> are not allowed as parameters in a <span class="CodeFont">CREATE FUNCTION</span> statement.

returnDataType

``` FcnSyntax
DataType |
TableType
```

functionElement

See the description of [Function Elements](#FunctionElements) in the next section.

[]()TableType

``` FcnSyntax
TABLE( ColumnElement [,ColumnElement]* )
```

ColumnElement

A <span class="ItalicFont">[DataType](../DataTypes/Intro.DataTypes.html)</span>or an <span class="ItalicFont">[SQL Identifier](../Identifiers/Intro.Identifiers.html)</span>.

Table functions return <span class="CodeFont">TableType</span> results. Currently, only Splice Machine-style table functions are supporte, which are functions that return JDBC <span class="ItalicFont">ResultSets.</span>

When values are extracted from a <span class="ItalicFont">ResultSet</span>, the data types of the values are coerced to match the data types declared in the <span class="CodeFont">CREATE FUNCTION </span>statement. Here are a few coercion rules you should know about:

-   values that are too long are truncated to the maximum declared length
-   if a string value is returned in the <span class="ItalicFont">ResultSet</span> for a column of type <span class="CodeFont">CHAR</span>, and the string is shorter than the column length, the string is padded with spaces

[]()Function Elements

``` FcnSyntax
 {
    LANGUAGE { JAVA }
  | DeterministicCharacteristic
  | EXTERNAL NAME javaMethodName
  | PARAMETER STYLE parameterStyle
  | sqlStatementType
  | nullInputAction
}
```

The function elements may appear in any order, but each type of element can only appear once.

These function elements are required:

-    <span class="ItalicFont">LANGUAGE</span>
-   <span class="ItalicFont">EXTERNAL NAME</span>
-   <span class="ItalicFont">PARAMETER STYLE</span>

LANGUAGE

Only <span class="CodeFont">JAVA</span> is accepted at this time. Splice Machine will call the function as a public static method in a Java class.

DeterministicCharacteristic

``` FcnSyntax
DETERMINISTIC | NOT DETERMINISTIC
```

The default value is <span class="CodeFont">NOT DETERMINISTIC</span>.

Specifying <span class="CodeFont">DETERMINISTIC</span> indicates that the function always returns the same result, given the same input values. This allows Splice Machine to call the function with greater efficiency; however, specifying this for a function that is actually non-deterministic will have the opposite effect -- efficiency of calls to the function will be reduced.

javaMethodName

``` FcnSyntax
class_name.method_name
```

This is the name of the Java method to call when this function executes.

parameterStyle

``` FcnSyntax
JAVA | DERBY_JDBC_RESULT_SET
```

Only use <span class="CodeFont">DERBY\_JDBC\_RESULT\_SET</span> if this is a Splice Machine-style table function that returns a [TableType](#TableType) result, and is mapped to a Java method that returns a JDBC <span class="ItalicFont">ResultSet</span>.

Otherwise, use <span class="CodeFont">JAVA</span>-style parameters, which means that a parameter-passing convention is used that conforms to the Java language and SQL Routines specification. <span class="CodeFont">INOUT</span> and <span class="CodeFont">OUT</span> parameters are passed as single entry arrays to facilitate returning values. Result sets can be returned through additional parameters to the Java method of type <span class="CodeFont">java.sql.ResultSet\[\]</span> that are passed single entry arrays.

Splice Machine does not support long column types such as <span class="CodeFont">LONG VARCHAR</span>or <span class="CodeFont">BLOB</span>; an error will occur if you try to use one of these long column types.

sqlStatementType

CONTAINS SQL

Indicates that SQL statements that neither read nor modify SQL data can be executed by the function. Statements that are not supported in any function return a different error.

NO SQL

Indicates that the function cannot execute any SQL statements

READS SQL DATA

Indicates that some SQL statements that do not modify SQL data can be included in the function. Statements that are not supported in any stored function return a different error. This is the default value.

nullInputAction

RETURNS NULL ON NULL INPUT

If any input argument is null, the function is not invoked, and the result is null.

CALLED ON NULL INPUT

This is the default value.

The function is invoked even if all input arguments are null, which means that the invoked function must test for null argument values.The result may be null or not null.

Example of declaring a scalar function

For more complete examples of using <span class="CodeFont">CREATE FUNCTION</span>, please see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section of our <span class="ItalicFont">Developer's Guide</span>.

``` Example
splice> CREATE FUNCTION TO_DEGREES( RADIANS DOUBLE )
  RETURNS DOUBLE
  PARAMETER STYLE JAVA
  NO SQL LANGUAGE JAVA
  EXTERNAL NAME 'java.lang.Math.toDegrees';

0 rows inserted/updated/deleted
```

Example of declaring a table function

This example reads data from a mySql database and inserts it into a Splice Machine database.

We first implement a class that contains a public static method that connects to an external (foreign) database, uses a prepared statement to pull results from it, and returns those results as a JDBC <span class="CodeFont">ResultSet</span>:

``` Example
package splicemachine.example.vti;
import java.sql.*;
public class EmployeeTable
{
   public static ResultSet read()
          throws SQLException
    {
        Connection conn DriverManager.getConnection( "jdbc:mysql://localhost/hr?user=myName&password=myPswd" );
        PreparedStatement ps = conn.prepareStatement( "SELECT * FROM hrSchema.EmployeeTable" );
        return ps.executeQuery();
    }
}
```

Next we use the <span class="CodeFont">[CREATE FUNCTION](#)</span> .statement to declare a table function to read data from our external database and insert it into our Splice Machine database:

``` Example
CREATE FUNCTION externalEmployees()
   RETURNS TABLE
     (
      employeeId    INT,
      lastName      VARCHAR( 50 ),
      firstName     VARCHAR( 50 ),
      birthday      DATE
     )
   LANGUAGE JAVA
   PARAMETER STYLE SPLICE_JDBC_RESULT_SET
   READS SQL DATA

   EXTERNAL NAME 'com.splicemachine.example.vti.readEmployees';
```

Now we're ready to invoke our table function to read data from the external database and insert it into a table in our Splice Machine database.

To invoke a table function, you must wrap it in a <span class="CodeFont">TABLE</span> constructor in the <span class="CodeFont">FROM</span> list of a query. For example, we could insert employee data from that database into a table named <span class="CodeFont">employees</span> in our Splice Machine database:

``` Example
INSERT INTO employees
  SELECT myExtTbl.*
    FROM TABLE (externalEmployees() ) myExtTbl;
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You <span class="BoldFont">MUST</span> specify the table alias when using a virtual table; for example, <span class="CodeFont">myExtTbl</span> in the above example.

See Also

-   [<span class="CodeFont">CREATE\_PROCEDURE</span>](CreateProcedure.html) statement
-   [<span class="CodeFont">CURRENT\_USER</span>](../BuiltInFcns/CurrentUser.html) function
-   [Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DROP FUNCTION</span>](DropFunction.html) statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   [SQL Identifier](../Identifiers/Intro.Identifiers.html)
-   [<span class="CodeFont">SESSION\_USER</span>](../BuiltInFcns/SessionUser.html) function
-   [<span class="CodeFont">USER</span>](../BuiltInFcns/User.html) function

 


