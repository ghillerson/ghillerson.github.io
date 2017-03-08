[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Intro.BuiltInFcns.html)

[]()Built-in SQL Functions
==========================

This section contains the reference documentation for the SQL Functions that are built into Splice Machine, which are grouped into the following subsections:

-   [Conversion Functions](Intro.ConversionFcns.html)
-   [Current Session Functions](Intro.CurrentSessionFcns.html)
-   [Date and Time Functions](Intro.DateTimeFcns.html)
-   [Miscellaneous Functions](Intro.MiscellaneousFcns.html)
-   [Numeric Functions](Intro.NumericFcns.html)
-   [String Functions](Intro.StringFcns.html)
-   [Trigonometric Functions](Intro.TrigonometricFncs.html)
-   [Window and Aggregate Functions](Intro.WindowAggregrateFcns.html)

Conversion Functions

These are the built-in [conversion functions](Intro.ConversionFcns.html):

| Function Name             | Description                                                                                                         |
|---------------------------|---------------------------------------------------------------------------------------------------------------------|
| [BIGINT](BigInt.html)     | Returns a 64-bit integer representation of a number or character string in the form of an integer constant.         |
| [CAST](Cast.html)         | Converts a value from one data type to another and provides a data type to a dynamic parameter (?) or a NULL value. |
| [CHAR](Char.html)         | Returns a fixed-length character string representation.                                                             |
| [DOUBLE](Double.html)     | Returns a floating-point number                                                                                     |
| [INTEGER](Integer.html)   | Returns an integer representation of a number or character string in the form of an integer constant.               |
| [SMALLINT](SmallInt.html) | Returns a small integer representation of a number or character string in the form of a small integer constant.     |
| [TO\_CHAR](ToChar.html)   | Formats a date value into a string.                                                                                 |
| [TO\_DATE](ToDate.html)   | Formats a date string according to a formatting specification, and returns a date value.                            |
| [VARCHAR](VarChar.html)   | Returns a varying-length character string representation of a character string.                                     |

Current Session Functions

These are the built-in [current session functions](Intro.CurrentSessionFcns.html):

| Function Name                        | Description                                                                                                                           |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| [CURRENT\_ROLE](CurrentRole.html)    | Returns the authorization identifier of the current role.                                                                             |
| [CURRENT SCHEMA](CurrentSchema.html) | Returns the schema name used to qualify unqualified database object references.                                                       |
| [CURRENT\_USER](CurrentUser.html)    | Depending on context, returns the authorization identifier of either the user who created the SQL session or the owner of the schema. |
| [SESSION\_USER](SessionUser.html)    | Depending on context, returns the authorization identifier of either the user who created the SQL session or the owner of the schema. |
| [USER](User.html)                    | Depending on context, returns the authorization identifier of either the user who created the SQL session or the owner of the schema. |

Date and Time Functions

These are the built-in [date and time functions](Intro.DateTimeFcns.html):

| Function Name                                                    | Description                                                                               |
|------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| [ADD\_MONTHS](AddMonths.html)                                    | Returns the date resulting from adding a number of months added to a specified date.      |
| [CURRENT\_DATE](CurrentDate.html)                                | Returns the current date.                                                                 |
| [CURRENT\_TIME](CurrentTime.html)                                | Returns the current time;                                                                 |
| [CURRENT\_TIMESTAMP](CurrentTimestamp.html)                      | Returns the current timestamp;                                                            |
| [DATE](Date.html)                                                | Returns a date from a value.                                                              |
| [DAY](Day.html)                                                  | Returns the day part of a value.                                                          |
| [EXTRACT](Extract.html)                                          | Extracts various date and time components from a date expression.                         |
| [HOUR](Hour.html)                                                | Returns the hour part of a value.                                                         |
| [LAST\_DAY](LastDay.html)                                        | Returns the date of the last day of the specified month.                                  |
| [MINUTE](Minute.html)                                            | Returns the minute part of a value.                                                       |
| [MONTH](Month.html)                                              | Returns the numeric month part of a value.                                                |
| [MONTH\_BETWEEN](MonthBetween.html)                              | Returns the number of months between two dates.                                           |
| [MONTHNAME](MonthName.html)                                      | Returns the string month part of a value.                                                 |
| [NEXT\_DAY](NextDay.html)                                        | Returns the date of the next specified day of the week after a specified date.            |
| [NOW](Now.html)                                                  | Returns the current date and time as a timestamp value.                                   |
| [QUARTER](Quarter.html)                                          | Returns the quarter number (1-4) from a date expression.                                  |
| [SECOND](Second.html)                                            | Returns the seconds part of a value.                                                      |
| [TIME](Time.html)                                                | Returns a time from a value.                                                              |
| [TIMESTAMP](TimeStamp.html)                                      | Returns a timestamp from a value or a pair of values.                                     |
| [TIMESTAMPADD](TimeStampAdd.html)                                | Adds the value of an interval to a timestamp value and returns the sum as a new timestamp |
| [TIMESTAMPDIFF](TimeStampDiff.html)                              | Finds the difference between two timestamps, in terms of the specfied interval.           |
| [TO\_CHAR](ToChar.html)                                          | Formats a date value into a string.                                                       |
| [TO\_DATE](ToDate.html)                                          | Formats a date string according to a formatting specification, and returns a date value.  |
| [TRUNC <span class="bodyFont">or</span> TRUNCATE](Truncate.html) | Truncates numeric, date, and timestamp values.                                            |
| [WEEK](Week.html)                                                | Returns the year part of a value.                                                         |
| [YEAR](Year.html)                                                | Returns the year part of a value.                                                         |

Miscellaneous Functions

These are the built-in [miscellaneous functions](Intro.MiscellaneousFcns.html):

| Function Name                                 | Description                                                                                            |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------|
| [COALESCE](Coalesce.html)                     | Takes two or more compatible arguments and Returns the first argument that is not null.                |
| [IDENTITY\_VAL\_LOCAL](IdentityValLocal.html) | Returns the most recently assigned value of an identity column for a connection.                       |
| [NULLIF](Nullif.html)                         | Returns NULL if the two arguments are equal, and it Returns the first argument if they are not equal.  |
| [ROWID](RowNumber.html)                       | A <span class="ItalicFont">pseudocolumn</span> that uniquely defines a single row in a database table. |

Numeric Functions

These are the built-in [numeric functions](Intro.NumericFcns.html):

| Function Name                                                    | Description                                                                                                          |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| [ABS <span class="bodyFont">or</span> ABSVAL](Abs.html)          | Returns the absolute value of a numeric expression.                                                                  |
| [CEIL <span class="bodyFont">or</span> CEILING](Ceil.html)       | Round the specified number up, and return the smallest number that is greater than or equal to the specified number. |
| [EXP](Exp.html)                                                  | Returns <span class="ItalicFont">e</span> raised to the power of the specified number.                               |
| [FLOOR](Floor.html)                                              | Rounds the specified number down, and Returns the largest number that is less than or equal to the specified number. |
| [LN <span class="bodyFont">or</span> LOG](LnOrLog.html)          | Return the natural logarithm (base e) of the specified number.                                                       |
| [LOG10](Log10.html)                                              | Returns the base-10 logarithm of the specified number.                                                               |
| [MOD](Mod.html)                                                  | Returns the remainder (modulus) of one number divided by another.                                                    |
| [RAND](Rand.html)                                                | Returns a random number given a seed number                                                                          |
| [RANDOM](Random.html)                                            | Returns a random number.                                                                                             |
| [SIGN](Sign.html)                                                | Returns the sign of the specified number.                                                                            |
| [SQRT](Sqrt.html)                                                | Returns the square root of a floating point number;                                                                  |
| [TRUNC <span class="bodyFont">or</span> TRUNCATE](Truncate.html) | Truncates numeric, date, and timestamp values.                                                                       |

String Functions

These are the built-in [string functions](Intro.StringFcns.html):

| Function Name                                              | Description                                                                                                                       |
|------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| [Concatenate](Concatenation.html)                          | Concatenates a character string value onto the end of another character string. Can also be used on bit string values.            |
| [INITCAP](InitCap.html)                                    | Converts the first letter of each word in a string to uppercase, and converts any remaining characters in each word to lowercase. |
| [INSTR](Instr.html)                                        | Returns the index of the first occurrence of a substring in a string.                                                             |
| [LCASE <span class="bodyFont">or</span> LOWER](LCase.html) | Takes a character expression as a parameter and Returns a string in which all alpha characters have been converted to lowercase.  |
| [LENGTH](Length.html)                                      | Applied to either a character string expression or a bit string expression and Returns the number of characters in the result.    |
| [LOCATE](Locate.html)                                      | Used to search for a string within another string.                                                                                |
| [LTRIM](LTrim.html)                                        | Removes blanks from the beginning of a character string expression.                                                               |
| [REGEXP\_LIKE](RegexpLike.html)                            | Returns true if a string matches a regular expression.                                                                            |
| [REPLACE](Replace.html)                                    | Replaces all occurrences of a substring with another substring                                                                    |
| [RTRIM](RTrim.html)                                        | Removes blanks from the end of a character string expression.                                                                     |
| [SUBSTR](Substr.html)                                      | Return a portion of string beginning at the specified position for the number of characters specified or rest of the string.      |
| [TRIM](Trim.html)                                          | Takes a character expression and Returns that expression with leading and/or trailing pad characters removed.                     |
| [UCASE <span class="bodyFont">or</span> UPPER](UCase.html) | Takes a character expression as a parameter and Returns a string in which all alpha characters have been converted to uppercase.  |

Trigonometric Functions

These are the built-in [trigonometric functions](Intro.DateTimeFcns.html):

| Function Name           | Description                                                               |
|-------------------------|---------------------------------------------------------------------------|
| [ACOS](Acos.html)       | Returns the arc cosine of a specified number.                             |
| [ASIN](Asin.html)       | Returns the arc sine of a specified number.                               |
| [ATAN](Atan.html)       | Returns the arc tangent of a specified number.                            |
| [ATAN2](Atan2.html)     | Returns the arctangent, in radians, of the quotient of the two arguments. |
| [COS](Cos.html)         | Returns the cosine of a specified number.                                 |
| [COSH](Cosh.html)       | Returns the hyperbolic cosine of a specified number.                      |
| [COT](Cot.html)         | Returns the cotangens of a specified number.                              |
| [DEGREES](Degrees.html) | Converts a specified number from radians to degrees.                      |
| [PI](Pi.html)           | Returns a value that is closer than any other value to pi.                |
| [RADIANS](Radians.html) | Converts a specified number from degrees to radians.                      |
| [SIN](Sin.html)         | Returns the sine of a specified number.                                   |
| [SINH](Sinh.html)       | Returns the hyperbolic sine of a specified number.                        |
| [TAN](Tan.html)         | Returns the tangent of a specified number.                                |
| [TANH](Tanh.html)       | Returns the hyperbolic tangent of a specified number                      |

Window and Aggregate Functions

These are the built-in [window and aggregate functions](Intro.WindowAggregrateFcns.html): 

| Function Name                                                 | Description                                                                                                                                              |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="CodeFont">[AVG](Avg.html)</span>                 | Returns the average computed over a subset (partition) of a table.                                                                                       |
| <span class="CodeFont">[COUNT](Count.html)</span>             | Returns the number of rows in a partition.                                                                                                               |
| <span class="CodeFont">[DENSE\_RANK](DenseRank.html)</span>   | Returns the ranking of a row within a partition.                                                                                                         |
| <span class="CodeFont">[FIRST\_VALUE](FirstValue.html)</span> | Returns the first value within a partition..                                                                                                             |
| <span class="CodeFont">[LAG](Lag.html)</span>                 | Returns the value of an expression evaluated at a specified offset number of rows <span class="ItalicFont">before</span> the current row in a partition. |
| <span class="CodeFont">[LAST\_VALUE](LastValue.html)</span>   | Returns the last value within a partition..                                                                                                              |
| <span class="CodeFont">[LEAD](Lead.html)</span>               | Returns the value of an expression evaluated at a specified offset number of rows <span class="ItalicFont">after</span> the current row in a partition.  |
| <span class="CodeFont">[MAX](Max.html)</span>                 | Returns the maximum value computed over a partition.                                                                                                     |
| <span class="CodeFont">[MIN](Min.html)</span>                 | Returns the minimum value computed over a partition.                                                                                                     |
| <span class="CodeFont">[RANK](Rank.html)</span>               | Returns the ranking of a row within a subset of a table.                                                                                                 |
| <span class="CodeFont">[ROW\_NUMBER](RowNumber.html)</span>   | Returns the row number of a row within a partition.                                                                                                      |
| [<span class="CodeFont">STDDEV\_POP</span>](StdDevPop.html)   | Returns the population standard deviation of a set of numeric values                                                                                     |
| [<span class="CodeFont">STDDEV\_SAMP</span>](StdDevSamp.html) | Returns the sample standard deviation of a set of numeric values                                                                                         |
| <span class="CodeFont">[SUM](Sum.html)</span>                 | Returns the sum of a value calculated over a partition.                                                                                                  |

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

 


