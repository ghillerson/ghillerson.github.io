[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Varchar.html)

<a href="" id="DataTypes.Varchar"></a>[]()VARCHAR
=================================================

The <span class="CodeFont">VARCHAR</span> data type provides for variable-length storage of strings.

Syntax

``` FcnSyntax
{ VARCHAR | CHAR VARYING | CHARACTER VARYING }(length)
```

length

An unsigned integer constant. The maximum length for a <span class="CodeFont">VARCHAR</span> string is <span class="CodeFont">32,672</span> characters.

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.String
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
VARCHAR
```

Example

``` Example
VARCHAR(2048);
```

Usage Notes

Here are several notes for the <span class="CodeFont">VARCHAR</span> data type:

-   Splice Machine does not pad a <span class="CodeFont">VARCHAR</span> value whose length is less than specified.
-   Splice Machine truncates spaces from a string value when a length greater than the <span class="CodeFont">VARCHAR</span> expected is provided. Characters other than spaces are not truncated, and instead cause an exception to be raised.
-   When [comparison boolean operators](../Expressions/BooleanExpressions.html) are applied to <span class="CodeFont">VARCHARs</span>, the lengths of the operands are not altered, and spaces at the end of the values are ignored.
-   When <span class="CodeFont">CHARs</span> and <span class="CodeFont">VARCHARs</span> are mixed in expressions, the shorter value is padded with spaces to the length of the longer value.
-   The type of a string constant is <span class="CodeFont">CHAR</span>, not <span class="CodeFont">VARCHAR</span>.

 


