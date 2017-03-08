[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Blob.html)

<a href="" id="DataTypes.Blob"></a>[]()BLOB
===========================================

A <span class="CodeFont">BLOB</span> (binary large object) value is a varying-length binary string that can be up to <span class="CodeFont">2,147,483,647</span> characters long.

Like other binary types, <span class="CodeFont">BLOB</span>strings are not associated with a code page. In addition, <span class="CodeFont">BLOB</span>strings do not hold character data.

Syntax

``` FcnSyntax
{BLOB | BINARY LARGE OBJECT} [ ( length [{K |M |G}] ) ]
```

length

An unsigned integer constant that specifies the number of characters in the <span class="CodeFont">BLOB</span> unless you specify one of the suffixes you see below, which change the meaning of the <span class="ItalicFont">length</span> value. If you do not specify a length value, it defaults to two gigabytes (2,147,483,647).

K

If specified, indicates that the length value is in multiples of 1024 (kilobytes).

M

If specified, indicates that the length value is in multiples of 1024\*1024 (megabytes).

G

If specified, indicates that the length value is in multiples of 1024\*1024\*1024 (gigabytes).

Corresponding Compile-time Java Type

``` FcnSyntax
java.sql.Blob
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
BLOB
```

Usage Notes

Use the <span class="ItalicFont">getBlob</span> method on the <span class="ItalicFont">java.sql.ResultSet</span> to retrieve a <span class="CodeFont">BLOB</span> handle to the underlying data.

There are a number of restrictions on using <span class="CodeFont">BLOB</span> and <span class="CodeFont">CLOB</span> / <span class="CodeFont">TEXT</span> objects, which we refer to as LOB-types:

-   LOB-types cannot be compared for equality (<span class="CodeFont">=</span>) and non-equality (<span class="CodeFont">!=</span>, <span class="CodeFont">&lt;&gt;</span>).
-   LOB-typed values cannot be ordered, so <span class="CodeFont">&lt;, &lt;=, &gt;, &gt;=</span> tests are not supported.
-   LOB-types cannot be used in indexes or as primary key columns.
-   <span class="CodeFont">DISTINCT</span>, <span class="CodeFont">GROUP BY</span>, and <span class="CodeFont">ORDER BY</span> clauses are also prohibited on LOB-types.
-   LOB-types cannot be involved in implicit casting as other base-types.

Example

Using an <span class="CodeFont">[INSERT](../Statements/Insert.html)</span> statement to put <span class="CodeFont">BLOB</span> data into a table has some limitations if you need to cast a long string constant to a <span class="CodeFont">BLOB</span>. You may be better off using a binary stream, as in the following code fragment.

 


