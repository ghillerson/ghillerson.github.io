[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Char.html)

<a href="" id="DataTypes.Char"></a>[]()CHAR
===========================================

The <span class="CodeFont">CHAR</span> data type provides for fixed-length storage of strings.

Syntax

``` FcnSyntax
CHAR[ACTER] [(length)]
```

length

An unsigned integer literal designating the length in bytes. The default <span class="ItalicFont">length</span> for a <span class="CodeFont">CHAR</span> is <span class="CodeFont">1</span>; the maximum size of <span class="ItalicFont">length</span> is <span class="CodeFont">254</span>..

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.String
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
CHAR
```

Usage Notes

Here are several usage notes for the <span class="CodeFont">CHAR</span> data type:

-   Splice Machine inserts spaces to pad a string value shorter than the expected length, and truncates spaces from a string value longer than the expected length. Characters other than spaces cause an exception to be raised. When [comparison boolean operators](../Expressions/BooleanExpressions.html) are applied to <span class="CodeFont">CHARs</span>, the shorter string is padded with spaces to the length of the longer string.
-   When <span class="CodeFont">CHARs</span> and <span class="CodeFont">VARCHARs</span> are mixed in expressions, the shorter value is padded with spaces to the length of the longer value.
-   The type of a string constant is <span class="CodeFont">CHAR</span>.

Examples

``` Example
   -- within a string constant use two single quotation marks
   -- to represent a single quotation mark or apostrophe 
VALUES 'hello this is Joe''s string';

   -- create a table with a CHAR field
CREATE TABLE STATUS (
    STATUSCODE CHAR(2) NOT NULL
        CONSTRAINT PK_STATUS PRIMARY KEY,
    STATUSDESC VARCHAR(40) NOT NULL
);    
```

 


