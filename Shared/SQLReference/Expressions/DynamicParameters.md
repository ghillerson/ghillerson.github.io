[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/DynamicParameters.html)

<a href="" id="Expressions.DynamicParameters"></a>[]()Dynamic Parameters
========================================================================

You can prepare statements that are allowed to have parameters for which the value is not specified when the statement is repared using <span class="ItalicFont">PreparedStatement</span> methods in the JDBC API. These parameters are called dynamic parameters and are represented by a ?.

The JDBC API documents refer to dynamic parameters as <span class="CodeFont">IN</span>, <span class="CodeFont">INOUT</span>, or <span class="CodeFont">OUT</span> parameters. In SQL, they are always <span class="CodeFont">IN</span> parameters.

You must specify values for dynamic parameters before executing the statement, and the types of the specified values must match the expected types.

Example

``` Example
PreparedStatement ps2 = conn.prepareStatement(
  "UPDATE HotelAvailability SET rooms_available = " +
  "(rooms_available - ?) WHERE hotel_id = ? " +
  "AND booking_date BETWEEN ? AND ?");

       -- this sample code sets the values of dynamic parameters
       -- to be the values of program variables
ps2.setInt(1, numberRooms);
ps2.setInt(2, theHotel.hotelId);
ps2.setDate(3, arrival);
ps2.setDate(4, departure);
updateCount = ps2.executeUpdate();
```

<a href="" id="DynamicParametersAllowed"></a>[]()Where Dynamic Parameters are Allowed

You can use dynamic parameters anywhere in an expression where their data type can be easily deduced.

-   Use as the first operand of <span class="CodeFont">BETWEEN</span> is allowed if one of the second and third operands is not also a dynamic parameter. The type of the first operand is assumed to be the type of the non-dynamic parameter, or the union result of their types if both are not dynamic parameters.
    ``` Example
    WHERE ? BETWEEN DATE('1996-01-01') AND ?
       -- types assumed to be DATE
    ```

-   Use as the second or third operand of <span class="CodeFont">BETWEEN</span> is allowed. Type is assumed to be the type of the left operand.
    ``` Example
    WHERE DATE('1996-01-01') BETWEEN ? AND ?
       -- types assumed to be DATE
    ```

-   Use as the left operand of an <span class="CodeFont">IN</span> list is allowed if at least one item in the list is not itself a dynamic parameter. Type for the left operand is assumed to be the union result of the types of the non-dynamic parameters in the list.
    ``` Example
    WHERE ? NOT IN (?, ?, 'Santiago')
       -- types assumed to be CHAR
    ```

-   Use in the values list in an <span class="CodeFont">IN</span> predicate is allowed if the first operand is not a dynamic parameter or its type was determined in the previous rule. Type of the dynamic parameters appearing in the values list is assumed to be the type of the left operand.
    ``` Example
    WHERE FloatColumn IN (?, ?, ?)
       -- types assumed to be FLOAT
    ```

-   For the binary operators <span class="CodeFont">+, -, \*, /, AND, OR, &lt;, &gt;, =, &lt;&gt;, &lt;=, and &gt;=,</span> use of a dynamic parameter as one operand but not both is permitted. Its type is taken from the other side.
    ``` Example
    WHERE ? < CURRENT_TIMESTAMP
       -- type assumed to be a TIMESTAMP
    ```

-   Use in a <span class="CodeFont">CAST</span> is always permitted. This gives the dynamic parameter a type.
    ``` Example
    CALL valueOf(CAST (? AS VARCHAR(10)))
    ```

-   Use on either or both sides of <span class="CodeFont">LIKE</span> operator is permitted. When used on the left, the type of the dynamic parameter is set to the type of the right operand, but with the maximum allowed length for the type. When used on the right, the type is assumed to be of the same length and type as the left operand. (<span class="CodeFont">LIKE</span> is permitted on <span class="CodeFont">CHAR</span> and <span class="CodeFont">VARCHAR</span> types; see [Concatenation operator](../BuiltInFcns/Concatenation.html) for more information.)
    ``` Example
    WHERE ? LIKE 'Santi%'
       -- type assumed to be CHAR with a length of
       -- java.lang.Integer.MAX_VALUE
    ```

-   In a conditional expression, which uses a <span class="CodeFont">?</span>, use of a dynamic parameter (which is also represented as a <span class="CodeFont">?</span>) is allowed. The type of a dynamic parameter as the first operand is assumed to be boolean. Only one of the second and third operands can be a dynamic parameter, and its type will be assumed to be the same as that of the other (that is, the third and second operand, respectively).
    ``` Example
    SELECT c1 IS NULL ? ? : c1
       -- allows you to specify a "default" value at execution time
       -- dynamic parameter assumed to be the type of c1
       -- you cannot have dynamic parameters on both sides
       -- of the :
    ```

-   A dynamic parameter is allowed as an item in the values list or select list of an <span class="CodeFont">INSERT</span> statement. The type of the dynamic parameter is assumed to be the type of the target column.
    ``` Example
    INSERT INTO t VALUES (?)
       -- dynamic parameter assumed to be the type
       -- of the only column in table t
    INSERT INTO t SELECT ?
    FROM t2
       -- not allowed
    ```

-   A <span class="CodeFont">?</span> parameter in a comparison with a subquery takes its type from the expression being selected by the subquery. For example:
    ``` Example
    SELECT *
    FROM tab1
    WHERE ? = (SELECT x FROM tab2)
    SELECT *
    FROM tab1
    WHERE ? = ANY (SELECT x FROM tab2)
       -- In both cases, the type of the dynamic parameter is
       -- assumed to be the same as the type of tab2.x.
    ```

-   A dynamic parameter is allowed as the value in an <span class="CodeFont">UPDATE</span> statement. The type of the dynamic parameter is assumed to be the type of the column in the target table.
    ``` Example
    UPDATE t2 SET c2 =?
       -- type is assumed to be type of c2
    ```

-   Dynamic parameters are allowed as the operand of the unary operators <span class="CodeFont">-</span> or <span class="CodeFont">+</span>. For example:
    ``` Example
    CREATE TABLE t1 (c11 INT, c12 SMALLINT, c13 DOUBLE, c14 CHAR(3))
    SELECT * FROM t1 WHERE c11 BETWEEN -? AND +?
       -- The type of both of the unary operators is INT
       -- based on the context in which they are used (that is,
       -- because c11 is INT, the unary parameters also get the 
       -- type INT.
    ```

-   <span class="CodeFont">LENGTH</span> allow a dynamic parameter. The type is assumed to be a maximum length <span class="CodeFont">VARCHAR</span> type.
    ``` Example
    SELECT LENGTH(?)
    ```

-   Qualified comparisons.
    ``` Example
    ? = SOME (SELECT 1 FROM t)
       -- is valid. Dynamic parameter assumed to be INTEGER type

    1 = SOME (SELECT ? FROM t)
       -- is valid. Dynamic parameter assumed to be INTEGER type.
    ```

-   A dynamic parameter is allowed as the left operand of an <span class="CodeFont">IS</span> expression and is assumed to be a <span class="CodeFont">Boolean</span>.

 


