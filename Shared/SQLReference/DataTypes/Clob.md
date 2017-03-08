[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Clob.html)

<a href="" id="DataTypes.Clob"></a> []()CLOB
============================================

A <span class="CodeFont">CLOB</span> (character large object) value can be up to 2,147,483,647 characters long. A <span class="CodeFont">CLOB</span> is used to store unicode character-based data, such as large documents in any character set.

Note that, in Splice Machine, <span class="CodeFont">TEXT</span> is a synonym for <span class="CodeFont">CLOB</span>, and that the documentation for the <span class="CodeFont">[TEXT](Text.html)</span> data type functionally matches the documentation for this topic. Splice Machine simply translates <span class="CodeFont">TEXT</span> into <span class="CodeFont">CLOB</span>.

Syntax

``` FcnSyntax
{CLOB | CHARACTER LARGE OBJECT} [ ( length [{K |M |G}] ) ]
```

length

An unsigned integer constant that specifies the number of characters in the <span class="CodeFont">CLOB</span> unless you specify one of the suffixes you see below, which change the meaning of the <span class="ItalicFont">length</span> value. If you do not specify a length value, it defaults to two giga-characters (2,147,483,647).

K

If specified, indicates that the length value is in multiples of 1024 (kilo-characters).

M

If specified, indicates that the length value is in multiples of 1024\*1024 (mega-characters).

G

If specified, indicates that the length value is in multiples of 1024\*1024\*1024 (giga-characters).

Corresponding Compile-time Java Type

``` FcnSyntax
java.sql.Clob
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
CLOB
```

Usage Notes

Use the <span class="ItalicFont">getClob</span> method on the <span class="ItalicFont">java.sql.ResultSet</span> to retrieve a <span class="CodeFont">CLOB</span> handle to the underlying data.

There are a number of restrictions on using using <span class="CodeFont">BLOB</span>and <span class="CodeFont">CLOB</span> / <span class="CodeFont">TEXT</span> objects, which we refer to as LOB-types:

-   LOB-types cannot be compared for equality (<span class="CodeFont">=</span>) and non-equality (<span class="CodeFont">!=</span>, <span class="CodeFont">&lt;&gt;</span>).
-   LOB-typed values cannot be ordered, so <span class="CodeFont">&lt;, &lt;=, &gt;, &gt;=</span> tests are not supported.
-   LOB-types cannot be used in indexes or as primary key columns.
-   <span class="CodeFont">DISTINCT</span>, <span class="CodeFont">GROUP BY</span>, and <span class="CodeFont">ORDER BY</span> clauses are also prohibited on LOB-types.
-   LOB-types cannot be involved in implicit casting as other base-types.

Example

``` Example
CREATE TABLE myTable( largeCol CLOB(65535));
```

 


