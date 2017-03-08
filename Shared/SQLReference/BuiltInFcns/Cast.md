[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Cast.html)

<a href="" id="BuiltInFcns.Cast"></a>[]()CAST
=============================================

The <span class="CodeFont">CAST</span> function converts a value from one data type to another and provides a data type to a dynamic parameter or a <span class="CodeFont">NULL</span> value.

<span class="CodeFont">CAST</span> expressions are permitted anywhere expressions are permitted.

Syntax

``` FcnSyntax
CAST ( [ Expression | NULL | ? ]
  AS Datatype)
```

The data type to which you are casting an expression is the <span class="ItalicFont">target type</span>. The data type of the expression from which you are casting is the <span class="ItalicFont">source type</span>.

CAST conversions among ANSI SQL data types

The following table shows valid explicit conversions between source types and target types for SQL data types. This table shows which explicit conversions between data types are valid. The first column on the table lists the source data types. The first row lists the target data types. A "Y" indicates that a conversion from the source to the target is valid. For example, the first cell in the second row lists the source data type SMALLINT. The remaining cells on the second row indicate the whether or not you can convert SMALLINT to the target data types that are listed in the first row of the table.

| TYPES        | B   
                O    
                O    
                L    
                E    
                A    
                N    | S   
                      M    
                      A    
                      L    
                      L    
                      I    
                      N    
                      T    | I   
                            N    
                            T    
                            E    
                            G    
                            E    
                            R    | B   
                                  I    
                                  G    
                                  I    
                                  N    
                                  T    | D   
                                        E    
                                        C    
                                        I    
                                        M    
                                        A    
                                        L    | R   
                                              E    
                                              A    
                                              L    | D   
                                                    O    
                                                    U    
                                                    B    
                                                    L    
                                                    E    | F   
                                                          L    
                                                          O    
                                                          A    
                                                          T    | C   
                                                                H    
                                                                A    
                                                                R    | V   
                                                                      A    
                                                                      R    
                                                                      C    
                                                                      H    
                                                                      A    
                                                                      R    | L   
                                                                            O    
                                                                            N    
                                                                            G    
                                                                            V    
                                                                            A    
                                                                            R    
                                                                            C    
                                                                            H    
                                                                            A    
                                                                            R    | C   
                                                                                  L    
                                                                                  O    
                                                                                  B    | B   
                                                                                        L    
                                                                                        O    
                                                                                        B    | D   
                                                                                              A    
                                                                                              T    
                                                                                              E    | T   
                                                                                                    I    
                                                                                                    M    
                                                                                                    E    | T   
                                                                                                          I    
                                                                                                          M    
                                                                                                          E    
                                                                                                          S    
                                                                                                          T    
                                                                                                          A    
                                                                                                          M    
                                                                                                          P    |
|--------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| BOOLEAN      | Y   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | -   | -   | -   |
| SMALLINT     | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   |
| INTEGER      | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   |
| BIGINT       | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   |
| DECIMAL      | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   |
| REAL         | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   |
| DOUBLE       | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   |
| FLOAT        | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   |
| CHAR         | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | Y   | Y   | Y   |
| VARCHAR      | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | Y   | Y   | Y   |
| LONG VARCHAR | Y   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | -   | -   | -   |
| CLOB         | Y   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | -   | -   | -   |
| BLOB         | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | Y   | -   | -   | -   |
| DATE         | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | -   | -   |
| TIME         | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | -   | Y   | -   |
| TIMESTAMP    | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | Y   | Y   |

If a conversion is valid, CASTs are allowed. Size incompatibilities between the source and target types might cause runtime errors.

Type Categories

This section lists information about converting specific data types. The Splice Machine ANSI SQL data types are categorized as follows:

| Category      | Data Types                                                                               |
|---------------|------------------------------------------------------------------------------------------|
| logical       | <span class="CodeFont">BOOLEAN</span>                                                    |
| numeric       | Exact numeric: <span class="CodeFont">SMALLINT, INTEGER, BIGINT, DECIMAL, NUMERIC</span> 
                                                                                                           
                 Approximate numeric: <span class="CodeFont">FLOAT, REAL, DOUBLE PRECISION</span>          |
| string        | Character string: <span class="CodeFont">CLOB, CHAR, VARCHAR, LONG VARCHAR</span>        
                                                                                                           
                 Bit string: <span class="CodeFont">BLOB</span>                                            |
| date and time | <span class="CodeFont">DATE, TIME, TIMESTAMP</span>                                      |

Conversion Notes

This section lists additional information about casting of certain data types.

Applying Multiple Conversions

As shown in the above table, you cannot convert freely among all types. For example, you cannot <span class="CodeFont">CAST</span>an <span class="CodeFont">INTEGER</span> value to a <span class="CodeFont">VARCHAR</span> value. However, you may be able to achieve your conversion by using multiple <span class="CodeFont">CAST</span> operations.

For example, since you can convert an <span class="CodeFont">INTEGER</span> value to a <span class="CodeFont">CHAR</span> value, and you can convert a <span class="CodeFont">CHAR</span> value to a <span class="CodeFont">VARCHAR</span> value, you can use multiple <span class="CodeFont">CAST</span> operations, as shown here:

``` Example
CAST(CAST(123 AS CHAR(10)) AS VARCHAR(10));

SELECT CAST(CAST(myId as CHAR(20)) as VARCHAR(20));
```

Conversions to and from logical types

These notes apply to converting logical values to strings and vice-versa:

-   A <span class="CodeFont">BOOLEAN</span> value can be cast explicitly to any of the string types. The result is <span class="CodeFont">'true'</span>, <span class="CodeFont">'false'</span>, or <span class="CodeFont">null</span>.
-   Conversely, string types can be cast to <span class="CodeFont">BOOLEAN</span>; however, an error is raised if the string value is not <span class="CodeFont">'true'</span>, <span class="CodeFont">'false'</span>, <span class="CodeFont">'unknown'</span>, or <span class="CodeFont">null</span>.
-   Casting <span class="CodeFont">'false'</span> to <span class="CodeFont">BOOLEAN</span> results in a <span class="CodeFont">null</span> value.

Conversions from numeric types

A numeric type can be converted to any other numeric type. These notes apply:

-   If the target type cannot represent the non-fractional component without truncation, an exception is raised.
-   If the target numeric cannot represent the fractional component (scale) of the source numeric, then the source is silently truncated to fit into the target. For example, casting <span class="CodeFont">763.1234</span> as <span class="CodeFont">INTEGER</span> yields <span class="CodeFont">763</span>.

Conversions from and to bit strings

Bit strings can be converted to other bit strings, but not to character strings. Strings that are converted to bit strings are padded with trailing zeros to fit the size of the target bit string. The <span class="CodeFont">BLOB</span> type is more limited and requires explicit casting. In most cases the <span class="CodeFont">BLOB</span> type cannot be cast to and from other types: you can cast a <span class="CodeFont">BLOB</span> only to another <span class="CodeFont">BLOB</span>, but you can cast other bit string types to a <span class="CodeFont">BLOB</span>.

Conversions of date/time values

A date/time value can always be converted to and from a <span class="CodeFont">TIMESTAMP</span>.

If a <span class="CodeFont">DATE</span> is converted to a <span class="CodeFont">TIMESTAMP</span>, the <span class="CodeFont">TIME</span> component of the resulting <span class="CodeFont">TIMESTAMP</span> is always <span class="CodeFont">00:00:00</span>.

If a <span class="CodeFont">TIME</span> data value is converted to a <span class="CodeFont">TIMESTAMP</span>, the <span class="CodeFont">DATE</span> component is set to the value of <span class="CodeFont">CURRENT\_DATE</span> at the time the <span class="CodeFont">CAST</span> is executed.

If a <span class="CodeFont">TIMESTAMP</span> is converted to a <span class="CodeFont">DATE</span>, the <span class="CodeFont">TIME</span> component is silently truncated.

If a <span class="CodeFont">TIMESTAMP</span> is converted to a <span class="CodeFont">TIME</span>, the <span class="CodeFont">DATE</span> component is silently truncated.

Examples

``` Example
splice> SELECT CAST (TotalBases AS BIGINT) 
  FROM Batting;

   -- convert timestamps to text  
splice> INSERT INTO mytable (text_column) 
  VALUES (CAST (CURRENT_TIMESTAMP AS VARCHAR(100)));

   -- you must cast NULL as a data type to use it
splice> SELECT airline
  FROM Airlines
  UNION ALL
  VALUES (CAST (NULL AS CHAR(2)));

   -- cast a double as a decimal
splice> SELECT CAST (FLYING_TIME AS DECIMAL(5,2))
  FROM FLIGHTS;

   -- cast a SMALLINT to a BIGINT
splice> VALUES CAST (CAST (12 as SMALLINT) as BIGINT);
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)

 


