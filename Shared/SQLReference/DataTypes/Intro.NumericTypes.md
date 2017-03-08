[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Intro.NumericTypes.html)

<a href="" id="DataTypes.AboutNumericTypes"></a>About []()Numeric Data Types
============================================================================

This section contains the reference documentation for the numeric data types built into Splice Machine SQL:

| Data Type                                | Description                                                                                                                                                                                                        |
|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BIGINT](BigInt.html)                    | The <span class="CodeFont">BIGINT</span> data type provides 8 bytes of storage for integer values.                                                                                                                 |
| [DECIMAL](Decimal.html)                  | The <span class="CodeFont">DECIMAL</span> data type provides an exact numeric in which the precision and scale can be arbitrarily sized.                                                                           
                                                                                                                                                                                                                                                                
                                            You can use <span class="CodeFont">DECIMAL</span> and <span class="CodeFont">NUMERIC</span> interchangeably.                                                                                                        |
| [DOUBLE](Double.html)                    | The <span class="CodeFont">DOUBLE</span> data type provides 8-byte storage for numbers using IEEE floating-point notation.                                                                                         
                                                                                                                                                                                                                                                                
                                            <span class="CodeFont">DOUBLE PRECISION</span> can be used synonymously with <span class="CodeFont">DOUBLE</span>.                                                                                                  |
| [DOUBLE PRECISION](DoublePrecision.html) | The <span class="CodeFont">DOUBLE PRECISION</span> data type provides 8-byte storage for numbers using IEEE floating-point notation.                                                                               
                                                                                                                                                                                                                                                                
                                            <span class="CodeFont">DOUBLE</span> can be used synonymously with <span class="CodeFont">DOUBLE PRECISION</span>.                                                                                                  |
| [FLOAT](Float.html)                      | The <span class="CodeFont">FLOAT</span> data type is an alias for either a <span class="CodeFont">REAL</span> or <span class="CodeFont">DOUBLE PRECISION</span> data type, depending on the precision you specify. |
| [INTEGER](Integer.html)                  | <span class="CodeFont">INTEGER</span> provides 4 bytes of storage for integer values.                                                                                                                              |
| [NUMERIC](Numeric.html)                  | The <span class="CodeFont">NUMERIC</span>data type provides an exact numeric in which the precision and scale can be arbitrarily sized.                                                                            
                                                                                                                                                                                                                                                                
                                            You can use <span class="CodeFont">NUMERIC</span> and <span class="CodeFont">DECIMAL</span> interchangeably.                                                                                                        |
| [REAL](Real.html)                        | The <span class="CodeFont">REAL</span> data type provides 4 bytes of storage for numbers using IEEE floating-point notation.                                                                                       |
| [SMALLINT](SmallInt.html)                | The <span class="CodeFont">SMALLINT</span> data type provides 2 bytes of storage.                                                                                                                                  |

Using Numeric Types
-------------------

Numeric types include the following types, which provide storage of varying sizes:

| Numeric Type                                      | Data Types                                                                                                                                                                                 |
|---------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integer numerics                                  | [<span class="CodeFont">SMALLINT</span>](SmallInt.html) (2 bytes)                                                                                                                          
                                                                                                                                                                                                                                                 
                                                     [<span class="CodeFont">INTEGER</span>](Integer.html) (4 bytes)                                                                                                                             
                                                                                                                                                                                                                                                 
                                                     [<span class="CodeFont">BIGINT</span>](BigInt.html) (8 bytes)                                                                                                                               |
| Floating-point (also called approximate) numerics | [<span class="CodeFont">REAL</span>](Real.html) (4 bytes)                                                                                                                                  
                                                                                                                                                                                                                                                 
                                                     [<span class="CodeFont">DOUBLE PRECISION</span>](DoublePrecision.html) (8 bytes)                                                                                                            
                                                                                                                                                                                                                                                 
                                                     [<span class="CodeFont">FLOAT</span>](Float.html) (an alias for [<span class="CodeFont">DOUBLE PRECISION</span>](DoublePrecision.html) or [<span class="CodeFont">REAL</span>](Real.html))  |
| Exact numerics                                    | [<span class="CodeFont">DECIMAL</span>](Decimal.html) (storage based on precision)                                                                                                         
                                                                                                                                                                                                                                                 
                                                     [<span class="CodeFont">NUMERIC</span>](Numeric.html) (an alias for [<span class="CodeFont">DECIMAL</span>](Decimal.html))                                                                  |

### <a href="" id="NumericTypePromotion"></a>Numeric Type Promotion in Expressions

The following table shows the result type of numeric expressions based on the mix of numeric data types in the expressions.

| Largest Type That Appears in Expression | Resulting Type of Expression |
|-----------------------------------------|------------------------------|
| DOUBLE PRECISION                        | DOUBLE PRECISION             |
| REAL                                    | DOUBLE PRECISION             |
| DECIMAL                                 | DECIMAL                      |
| BIGINT                                  | BIGINT                       |
| INTEGER                                 | INTEGER                      |
| SMALLINT                                | INTEGER                      |

For example:

``` Example
   -- returns a double precision value
VALUES 1 + 1.0e0;
   -- returns a decimal value
VALUES 1 + 1.0;
   -- returns an integer value
VALUES CAST (1 AS INT) + CAST (1 AS INT);
```

### <a href="" id="StoringValues"></a>Storing Numeric Values

An attempt to put a floating-point type of a larger storage size into a location of a smaller size fails only if the value cannot be stored in the smaller-size location. For example:

``` Example
create table mytable (r REAL, d DOUBLE PRECISION);
   0 rows inserted/updated/deleted
INSERT INTO mytable (r, d) values (3.4028236E38, 3.4028235E38);
   ERROR X0X41: The number '3.4028236E38' is outside the range for the data type REAL.
```

You can store a floating point type in an <span class="CodeFont">INTEGER</span> column; the fractional part of the number is truncated. For example:

``` Example
INSERT INTO mytable(integer_column) values (1.09e0);
   1 row inserted/updated/deleted
   SELECT integer_column
   FROM mytable;
---------------
   1
```

Integer types can always be placed successfully in approximate numeric values, although with the possible loss of some precision.

Integers can be stored in decimals if the <span class="CodeFont">DECIMAL</span> precision is large enough for the value. For example:

``` Example
ij>
insert into mytable (decimal_column) VALUES (55555555556666666666);
   ERROR X0Y21: The number '55555555556666666666' is outside the
   range of the target DECIMAL/NUMERIC(5,2) datatype.   
```

An attempt to put an integer value of a larger storage size into a location of a smaller size fails if the value cannot be stored in the smaller-size location. For example:

``` Example
INSERT INTO mytable (int_column) values 2147483648;
   ERROR 22003: The resulting value is outside the range for the data type INTEGER.
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> Splice Machine rounds down when truncating trailing digits from a <span class="CodeFont">NUMERIC</span> value.

### <a href="" id="Scale"></a>Scale for Decimal Arithmetic

SQL statements can involve arithmetic expressions that use decimal data types of different <span class="ItalicFont">precisions</span> (the total number of digits, both to the left and to the right of the decimal point) and <span class="ItalicFont">scales</span> (the number of digits of the fractional component).

The precision and scale of the resulting decimal type depend on the precision and scale of the operands.

Given an arithmetic expression that involves two decimal operands:

-   <span class="ItalicFont">lp</span> stands for the precision of the left operand
-   <span class="ItalicFont">rp</span> stands for the precision of the right operand
-   <span class="ItalicFont">ls</span> stands for the scale of the left operand
-   <span class="ItalicFont">rs</span> stands for the scale of the right operand

Use the following formulas to determine the scale of the resulting data type for the following kinds of arithmetical expressions:

| Operation                           | Scale               |
|-------------------------------------|---------------------|
| multiplication                      | ls + rs             |
| division                            | 31 - lp + ls - rs   |
| <span class="CodeFont">AVG()</span> | max(max(ls, rs), 4) |
| all others                          | max(ls, rs)         |

For example, the scale of the resulting data type of the following expression is <span class="Example">27</span>:

``` Example
11.0/1111.33
   // 31 - 3 + 1 - 2 = 2
```

Use the following formulas to determine the precision of the resulting data type for the following kinds of arithmetical expressions:

| Operation      | Precision                               |
|----------------|-----------------------------------------|
| multiplication | lp + rp                                 |
| addition       | 2 \* (p - s) + s                        |
| division       | lp - ls + rp + max(ls + rp - rs + 1, 4) |
| all others     | max(lp - ls, rp - rs) + 1 + max(ls, rs) |

See Also

-   [Data Type Compatability](DataTypeCompatability.html)
-   [<span class="CodeFont">BIGINT</span>](BigInt.html) data type
-   [<span class="CodeFont">BLOB</span>](Blob.html) data type
-   [<span class="CodeFont">BOOLEAN</span>](Boolean.html) data type
-   [<span class="CodeFont">CHAR</span>](Char.html) data type
-   [<span class="CodeFont">CLOB</span>](Clob.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) data type
-   [<span class="CodeFont">DECIMAL</span>](Decimal.html) data type
-   [<span class="CodeFont">DOUBLE</span>](Double.html) data type
-   [<span class="CodeFont">DOUBLE PRECISION</span>](DoublePrecision.html) data type
-   [<span class="CodeFont">FLOAT</span>](Float.html) data type
-   [<span class="CodeFont">INTEGER</span>](Integer.html) data type
-   [<span class="CodeFont">LONG VARCHAR</span>](LongVarchar.html) data type
-   [<span class="CodeFont">NUMERIC</span>](Numeric.html) data type
-   [<span class="CodeFont">REAL</span>](Real.html) data type
-   [<span class="CodeFont">SMALLINT</span>](SmallInt.html) data type
-   <span class="CodeFont">[TEXT](Text.html)</span> data type
-   [<span class="CodeFont">TIME</span>](Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) data type
-   [<span class="CodeFont">VARCHAR</span>](Varchar.html) data type

 


