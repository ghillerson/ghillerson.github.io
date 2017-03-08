[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Intro.DataTypes.html)

[]()Data Types[]()
==================

The SQL type system is used by the language compiler to determine the compile-time type of an expression and by the language execution system to determine the runtime type of an expression, which can be a subtype or implementation of the compile-time type.

Each type has associated with it values of that type. In addition, values in the database or resulting from expressions can be <span class="CodeFont">NULL</span>, which means the value is missing or unknown. Although there are some places where the keyword <span class="CodeFont">NULL</span> can be explicitly used, it is not in itself a value, because it needs to have a type associated with it.

This section contains the reference documentation for the Splice Machine SQL Data Types, in the following subsections:

-   [Character String Data Types](#Characte)
-   [Date and Time Data Types](#Date)
-   [Large Object Binary (LOB) Data Types](#Large)
-   [Numeric Data Types](#Numeric)
-   [Other Data Types](#Other)

[]()Character String Data Types

These are the [character string data types](Intro.CharStringDataTypes.html):

| Data Type                        | Description                                                                                                                                                                                                                                                                       |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [CHAR](Char.html)                | The <span class="CodeFont">CHAR</span> data type provides for fixed-length storage of strings.                                                                                                                                                                                    |
| [LONG VARCHAR](LongVarchar.html) | The <span class="CodeFont">LONG VARCHAR</span> type allows storage of character strings with a maximum length of 32,700 characters. It is identical to <span class="CodeFont">VARCHAR</span>, except that you cannot specify a maximum length when creating columns of this type. |
| [VARCHAR](Varchar.html)          | The <span class="CodeFont">VARCHAR</span> data type provides for variable-length storage of strings.                                                                                                                                                                              |

[]()Date and Time Data Types

These are the [date and time data types](Intro.DateTimeDataTypes.html):

| Data Type                   | Description                                                                                                                                                                                                          |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [DATE](Date.html)           | The <span class="CodeFont">DATE</span> data type provides for storage of a year-month-day in the range supported by <span class="ItalicFont">java.sql.Date</span>.                                                   |
| [TIME](Time.html)           | The <span class="CodeFont">TIME</span> data type provides for storage of a time-of-day value.                                                                                                                        |
| [TIMESTAMP](TimeStamp.html) | The <span class="CodeFont">TIMESTAMP</span> data type stores a combined <span class="CodeFont">DATE</span> and <span class="CodeFont">TIME</span> value, and allows a fractional-seconds value of up to nine digits. |

[]()Large Object Binary (LOB) Data Types

These are the [LOB data types](Intro.LOBDataTypes.html):

| Data Type                                       | Description                                                                                                                                                             |
|-------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BLOB](Blob.html)                               | The <span class="CodeFont">BLOB</span> (binary large object) data type is used for varying-length binary strings that can be up to 2,147,483,647 characters long.       |
| [CLOB](Clob.html)                               | The <span class="CodeFont">CLOB</span> (character large object) data type is used for varying-length character strings that can be up to 2,147,483,647 characters long. |
| <span class="CodeFont">[TEXT](Text.html)</span> | Exactly the same as <span class="CodeFont">CLOB</span>.                                                                                                                 |

[]()Numeric Data Types

These are the [numeric data types](Intro.NumericTypes.html):

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

[]()Other Data Types

These are the [other data types](Intro.OtherDataTypes.html):

| Data Type               | Description                                    |
|-------------------------|------------------------------------------------|
| [BOOLEAN](Boolean.html) | Provides 1 byte of storage for logical values. |

See Also

-   [Argument Matching](../ArgMatching/ArgumentMatching.html)
-   [Assignments](DataTypeCompatability.html)
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

 


