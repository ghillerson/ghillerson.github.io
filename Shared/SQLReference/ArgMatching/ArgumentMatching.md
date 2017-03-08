[Open topic with navigation](../../../index.html#Shared/SQLReference/ArgMatching/ArgumentMatching.html)

<a href="" id="SQLArgumentMatching"></a>[]()Argument Matching in Splice Machine
===============================================================================

When you declare a function or procedure using <span class="CodeFont">CREATE FUNCTION/PROCEDURE</span>, Splice Machine does not verify whether a matching Java method exists. Instead, Splice Machine looks for a matching method only when you invoke the function or procedure in a later SQL statement.

At that time, Splice Machine searches for a public, static method having the class and method name declared in the <span class="CodeFont">EXTERNAL NAME </span>clause of the earlier <span class="CodeFont">CREATE FUNCTION/PROCEDURE</span> statement. Furthermore, the Java types of the method's arguments and return value must match the SQL types declared in the <span class="CodeFont">CREATE FUNCTION/PROCEDURE </span>statement.

The following may happen:

| Result    | Description                                                         |
|-----------|---------------------------------------------------------------------|
| Success   | If exactly one Java method matches, then Splice Machine invokes it. |
| Ambiguity | If exactly one Java method matches, then Splice Machine invokes it. |
| Failure   | Splice Machine also raises an error if no method matches.           |

In mapping SQL data types to Java data types, Splice Machine considers the following kinds of matches:

Result
Description
 
Primitive Match
Splice Machine looks for a primitive Java type corresponding to the SQL type. For instance, SQL <span class="CodeFont">INTEGER </span>matches Java <span class="ItalicFont">int</span>
Wrapper Match
Splice Machine looks for a wrapper class in the <span class="ItalicFont">java.lang</span> or <span class="ItalicFont">java.sql</span> packages corresponding to the SQL type. For instance, SQL INTEGER matches <span class="ItalicFont">java.lang.Integer</span>. For a user-defined type (UDT), Splice Machine looks for the UDT's external name class.
Array Match
For <span class="CodeFont">OUT</span> and <span class="CodeFont">INOUT</span> procedure arguments, Splice Machine looks for an array of the corresponding primitive or wrapper type. For example, an <span class="CodeFont">OUT</span> procedure argument of type SQL <span class="CodeFont">INTEGER </span>matches <span class="ItalicFont">int\[\]</span> and <span class="ItalicFont">Integer\[\]</span>.
ResultSet Match
If a procedure is declared to return <span class="ItalicFont">n</span> RESULT SETS, Splice Machine looks for a method whose last <span class="ItalicFont">n</span> arguments are of type <span class="ItalicFont">java.sql.ResultSet\[\]</span>.
Splice Machine resolves function and procedure invocations as follows:

| Call type | Resolution                                                                                                                                                                                                                               |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Function  | Splice Machine looks for a method whose argument and return types are <span class="ItalicFont">primitive match</span>es or <span class="ItalicFont">wrapper match</span>es for the function's SQL arguments and return value.            |
| Procedure | Splice Machine looks for a method which returns void and whose argument types match as follows:                                                                                                                                          
                                                                                                                                                                                                                                                       
             -   <span class="CodeFont">IN</span> - Method arguments are <span class="ItalicFont">primitive match</span>es or <span class="ItalicFont">wrapper matches</span> for the procedure's <span class="CodeFont">IN</span> arguments.          
             -   <span class="CodeFont">OUT and INOUT</span> - Method arguments are <span class="ItalicFont">array match</span>es for the procedure's <span class="CodeFont">OUT</span> and <span class="CodeFont">INOUT</span> arguments.             
                                                                                                                                                                                                                                                       
             In addition, if the procedure returns <span class="ItalicFont">n</span> RESULT SETS, then the last <span class="ItalicFont">n</span> arguments of the Java method must be of type <span class="ItalicFont">java.sql.ResultSet\[\]</span>  |

Example of argument matching
----------------------------

The following function:

``` Example
CREATE FUNCTION TO_DEGREES
     ( RADIANS DOUBLE )
RETURNS DOUBLE
PARAMETER STYLE JAVA
NO SQL LANGUAGE JAVA
EXTERNAL NAME 'example.MathUtils.toDegrees'
;
```

would match all of the following methods:

``` Example
public static double toDegrees( double arg ) {...}
public static Double toDegrees( double arg ) {...}
public static double toDegrees( Double arg ) {...}
public static Double toDegrees( Double arg ) {...}
        
```

Note that Splice Machine raises an exception if it finds more than one matching method.

Mapping SQL data types to Java data types
-----------------------------------------

The following table shows how Splice Machine maps specific SQL data types to Java data types.

| SQL Type          | Primitive Match                         | Wrapper Match                                        |
|-------------------|-----------------------------------------|------------------------------------------------------|
| BOOLEAN           | <span class="ItalicFont">boolean</span> | <span class="ItalicFont">java.lang.Boolean</span>    |
| SMALLINT          | <span class="ItalicFont">short</span>   | <span class="ItalicFont">java.lang.Integer</span>    |
| INTEGER           | <span class="ItalicFont">int</span>     | <span class="ItalicFont">java.lang.Integer</span>    |
| BIGINT            | <span class="ItalicFont">long</span>    | <span class="ItalicFont">java.lang.Long</span>       |
| DECIMAL           | None                                    | <span class="ItalicFont">java.math.BigDecimal</span> |
| NUMERIC           | None                                    | <span class="ItalicFont">java.math.BigDecimal</span> |
| REAL              | <span class="ItalicFont">float</span>   | <span class="ItalicFont">java.lang.Float</span>      |
| DOUBLE            | <span class="ItalicFont">double</span>  | <span class="ItalicFont">java.lang.Double</span>     |
| FLOAT             | <span class="ItalicFont">double</span>  | <span class="ItalicFont">java.lang.Double</span>     |
| CHAR              | None                                    | <span class="ItalicFont">java.lang.String</span>     |
| VARCHAR           | None                                    | <span class="ItalicFont">java.lang.String</span>     |
| LONG VARCHAR      | None                                    | <span class="ItalicFont">java.lang.String</span>     |
| CLOB              | None                                    | <span class="ItalicFont">java.sql.Clob</span>        |
| BLOB              | None                                    | <span class="ItalicFont">java.sql.Blob</span>        |
| DATE              | None                                    | <span class="ItalicFont">java.sql.Date</span>        |
| TIME              | None                                    | <span class="ItalicFont">java.sql.Time</span>        |
| TIMESTAMP         | None                                    | <span class="ItalicFont">java.sql.Timestamp</span>   |
| User-defined type | None                                    | Underlying Java class                                |

See Also

-   [About Data Types](../DataTypes/Intro.DataTypes.html)

 


