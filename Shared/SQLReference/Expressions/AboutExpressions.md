[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/AboutExpressions.html)

<a href="" id="Expressions.AboutExpressions"></a>About []()Expressions
======================================================================

Syntax for many statements and expressions includes the term <span class="ItalicFont">Expression</span>, or a term for a specific kind of expression such as TableSubquery. Expressions are allowed in these specified places within statements.

Some locations allow only a specific type of expression or one with a specific property. If not otherwise specified, an expression is permitted anywhere the word <span class="ItalicFont">Expression</span> appears in the syntax. This includes:

-   [<span class="CodeFont">ORDER BY</span> clause](../Clauses/OrderBy.html)
-   <span class="CodeFont">[SelectExpression](Select.html)</span>
-   [<span class="CodeFont">UPDATE</span> statement](../Statements/UpdateTable.html) (SET portion)
-   [<span class="CodeFont">VALUES</span> Expression](Values.html)
-   [<span class="CodeFont">WHERE</span> clause](../Clauses/Where.html)

Of course, many other statements include these elements as building blocks, and so allow expressions as part of these elements.

The following tables list all the possible SQL expressions and indicate where the expressions are allowed.

[]()General Expressions

General expressions are expressions that might result in a value of any type. The following table lists the types of general expressions.

| <span class="BoldFont">Expression Type</span> | <span class="BoldFont">Explanation</span>                                                                                                                                                                                                                                                                                                                     |
|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Column reference                              | A [column-Name](../Identifiers/IdentifierTypes.html#ColumnName) that references the value of the column made visible to the expression containing the Column reference.                                                                                                                                                                                       
                                                 You must qualify the column-Name by the table name or correlation name if it is ambiguous.                                                                                                                                                                                                                                                                     
                                                                                                                                                                                                                                                                                                                                                                                                                
                                                 The qualifier of a column-Name must be the correlation name, if a correlation name is given to a table that is in a [<span class="CodeFont">FROM</span> clause](../Clauses/From.html). The table name is no longer visible as a <span class="ItalicFont">column-Name</span> qualifier once it has been aliased by a correlation name.                          
                                                                                                                                                                                                                                                                                                                                                                                                                
                                                 Allowed in <span class="ItalicFont">[SelectExpressions](Select.html)</span>, <span class="CodeFont">UPDATE</span> statements, and the <span class="CodeFont">WHERE</span> clauses of data manipulation statements.                                                                                                                                             |
| Constant                                      | Most built-in data types typically have constants associated with them (as shown in the Data types section).                                                                                                                                                                                                                                                  |
| <span class="CodeFont">NULL</span>            | <span class="CodeFont">NULL</span> is an untyped constant representing the unknown value.                                                                                                                                                                                                                                                                     
                                                 Allowed in <span class="CodeFont">[CAST](../BuiltInFcns/Cast.html)</span> expressions or in <span class="CodeFont">INSERT VALUES</span> lists and <span class="CodeFont">UPDATE SET</span> clauses. Using it in a <span class="CodeFont">CAST</span> expression gives it a specific data type.                                                                 |
| Dynamic parameter                             | A dynamic parameter is a parameter to an SQL statement for which the value is not specified when the statement is created. Instead, the statement has a question mark (?) as a placeholder for each dynamic parameter. See [Dynamic parameters](DynamicParameters.html).                                                                                      
                                                 Dynamic parameters are permitted only in prepared statements. You must specify values for them before the prepared statement is executed. The values specified must match the types expected.                                                                                                                                                                  
                                                                                                                                                                                                                                                                                                                                                                                                                
                                                 Allowed anywhere in an expression where the data type can be easily deduced. See [Dynamic parameters](DynamicParameters.html).                                                                                                                                                                                                                                 |
| <span class="CodeFont">CAST</span> expression | Allows you to specify the type of NULL or of a dynamic parameter or convert a value to another type. See [<span class="CodeFont">CAST</span> function](../BuiltInFcns/Cast.html).                                                                                                                                                                             |
| Scalar subquery                               | Subquery that returns a single row with a single column. See <span class="ItalicFont">[ScalarSubquery](../Queries/ScalarSubquery.html).</span>                                                                                                                                                                                                                |
| Table subquerry                               | Subquery that returns more than one column and more than one row. See <span class="ItalicFont">[TableSubquery](../Queries/TableSubquery.html).</span>                                                                                                                                                                                                         
                                                 Allowed as a tableExpression in a FROM clause and with EXISTS, IN, and quantified comparisons.                                                                                                                                                                                                                                                                 |
| Conditional expression                        | A conditional expression chooses an expression to evaluate based on a boolean test. Conditional expressions include the [<span class="CodeFont">CASE</span> expression](Case.html), the [<span class="CodeFont">NULLIF</span> function](../BuiltInFcns/Nullif.html), and the [<span class="CodeFont">COALESCE</span> function](../BuiltInFcns/Coalesce.html). |

Boolean Expressions

[Boolean expressions](BooleanExpressions.html) are expressions that result in boolean values. Most general expressions can result in boolean values. Boolean expressions commonly used in a WHERE clause are made of operands operated on by SQL operators.

[]()Numeric Expressions

Numeric expressions are expressions that result in numeric values. Most of the general expressions can result in numeric values. Numeric values have one of the following types:

-   BIGINT
-   DECIMAL
-   DOUBLE PRECISION
-   INTEGER
-   REAL
-   SMALLINT

The following table lists the types of numeric expressions.

| <span class="BoldFont">Expression Type</span>                                                                                        | <span class="BoldFont">Explanation</span>                                                                                                                                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="CodeFont">+</span>, <span class="CodeFont">-</span>, <span class="CodeFont">\*</span>, <span class="CodeFont">/</span>, 
 unary <span class="CodeFont">+</span> and <span class="CodeFont">-</span> expressions                                                 | Evaluate the expected math operation on the operands. If both operands are the same type, the result type is not promoted, so the division operator on integers results in an integer that is the truncation of the actual numeric result. When types are mixed, they are promoted as described in the Data types section. 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                    
                                                                                                                                        Unary <span class="CodeFont">+</span> is a noop (i.e., +4 is the same as 4).                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                                                                                                                                                                                                    
                                                                                                                                        Unary <span class="CodeFont">-</span> is the same as multiplying the value by -1, effectively changing its sign.                                                                                                                                                                                                            |
| AVG                                                                                                                                  | [<span class="CodeFont">AVG</span>](../BuiltInFcns/Avg.html) function                                                                                                                                                                                                                                                      |
| SUM                                                                                                                                  | [<span class="CodeFont">SUM</span>](../BuiltInFcns/Sum.html) function                                                                                                                                                                                                                                                      |
| LENGTH                                                                                                                               | [<span class="CodeFont">LENGTH</span>](../BuiltInFcns/Length.html) function.                                                                                                                                                                                                                                               |
| LOWER                                                                                                                                | [<span class="CodeFont">LCASE</span>](../BuiltInFcns/LCase.html) or <span class="CodeFont">[LOWER](../BuiltInFcns/LCase.html)</span> function.                                                                                                                                                                             |
| COUNT                                                                                                                                | [<span class="CodeFont">COUNT</span>](../BuiltInFcns/Count.html) function, including <span class="CodeFont">COUNT(\*).</span>                                                                                                                                                                                              |

[]()Character expressions

Character expressions are expressions that result in a <span class="CodeFont">CHAR</span> or <span class="CodeFont">VARCHAR</span> value. Most general expressions can result in a <span class="CodeFont">CHAR</span> or <span class="CodeFont">VARCHAR</span> value. The following table lists the types of character expressions.

| <span class="BoldFont">Expression Type</span>                                                            | <span class="BoldFont">Explanation</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| A <span class="CodeFont">CHAR</span> or <span class="CodeFont">VARCHAR</span> value that uses wildcards. | The wildcards <span class="CodeFont">%</span> and <span class="CodeFont">\_</span> make a character string a pattern against which the <span class="CodeFont">LIKE</span> operator can look for a match.                                                                                                                                                                                                                                                                                                                                                       |
| Concatenation expression                                                                                 | In a concatenation expression, the concatenation operator, <span class="CodeFont">||</span>, concatenates its right operand to the end of its left operand. Operates on character and bit strings. See [Concatenation operator](../BuiltInFcns/Concatenation.html).                                                                                                                                                                                                                                                                                            |
| Built-in string functions                                                                                | The built-in string functions act on a String and return a string. See [<span class="CodeFont">LTRIM function</span>](../BuiltInFcns/LTrim.html), [<span class="CodeFont">LCASE or LOWER function</span>](../BuiltInFcns/LCase.html), [<span class="CodeFont">RTRIM function</span>](../BuiltInFcns/RTrim.html), [<span class="CodeFont">TRIM function</span>](../BuiltInFcns/Trim.html), [<span class="CodeFont">SUBSTR function</span>](../BuiltInFcns/Substr.html), and [<span class="CodeFont">UCASE or UPPER function</span>](../BuiltInFcns/UCase.html). |

[]()Date and Time Expressions

A date or time expression results in a <span class="CodeFont">DATE</span>, <span class="CodeFont">TIME</span>, or <span class="CodeFont">TIMESTAMP</span> value. Most of the general expressions can result in a date or time value. The following table lists the types of date and time expressions.

| <span class="BoldFont">Expression Type</span> | <span class="BoldFont">Explanation</span>                                                                                                 |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| CURRENT\_DATE                                 | Returns the current date. See the [<span class="CodeFont">CURRENT\_DATE</span>](../BuiltInFcns/CurrentDate.html) function.                |
| CURRENT\_TIME                                 | Returns the current time. See the [<span class="CodeFont">CURRENT\_TIME</span>](../BuiltInFcns/CurrentTime.html) function.                |
| CURRENT\_TIMESTAMP                            | Returns the current timestamp. See the [<span class="CodeFont">CURRENT\_TIMESTAMP</span>](../BuiltInFcns/CurrentTimestamp.html) function. |

See Also

-   [<span class="CodeFont">AVG</span>](../BuiltInFcns/Avg.html) function
-   [<span class="CodeFont">CAST</span>](../BuiltInFcns/Cast.html) function
-   [<span class="CodeFont">COUNT</span>](../BuiltInFcns/Count.html) function
-   [<span class="CodeFont">CURRENT\_DATE</span>](../BuiltInFcns/CurrentDate.html) function
-   [<span class="CodeFont">CURRENT\_TIME</span>](../BuiltInFcns/CurrentTime.html) function
-   [<span class="CodeFont">CURRENT\_TIMESTAMP</span>](../BuiltInFcns/CurrentTimestamp.html) function
-   [<span class="CodeFont">Concatenation</span>](../BuiltInFcns/Concatenation.html) operator
-   [<span class="CodeFont">LCASE</span>](../BuiltInFcns/LCase.html) function
-   [<span class="CodeFont">LENGTH</span>](../BuiltInFcns/Length.html) function
-   [<span class="CodeFont">LTRIM</span>](../BuiltInFcns/LTrim.html) function
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">RTRIM</span>](../BuiltInFcns/RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](../BuiltInFcns/Substr.html) function
-   [<span class="CodeFont">SUM</span>](../BuiltInFcns/Sum.html) function
-   [<span class="CodeFont">Select</span>](Select.html) expression
-   [<span class="CodeFont">TRIM</span>](../BuiltInFcns/Trim.html) function
-   [<span class="CodeFont">UPDATE</span>](../Statements/UpdateTable.html) statement
-   [<span class="CodeFont">VALUES</span>](Values.html) expression
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


