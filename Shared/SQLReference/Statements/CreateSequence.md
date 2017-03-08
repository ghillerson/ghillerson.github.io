[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateSequence.html)

<a href="" id="Statements.CreateSequence"></a>[]()CREATE SEQUENCE
=================================================================

The <span class="CodeFont">CREATE SEQUENCE</span> statement creates a sequence generator, which is a mechanism for generating exact numeric values, one at a time.

Syntax

``` FcnSyntax
CREATE SEQUENCE 
   [ schemaName. ]SQL Identifier 
   [ sequenceElement ]*
```

The sequence name is composed of an optional <span class="ItalicFont">schemaName</span> and a <span class="ItalicFont">SQL Identifier</span>. If a <span class="ItalicFont">schemaName</span> is not provided, the current schema is the default schema. If a qualified sequence name is specified, the schema name cannot begin with SYS.

schemaName

The name of the schema to which this sequence belongs. If you do not specify a schema name, the current schema is assumed.

You cannot use a schema name that begins with the <span class="CodeFont">SYS.</span> prefix.

SQL Identifier

The name of the sequence

sequenceElement

``` FcnSyntax
{
  AS dataType 
   | START WITH startValue 
   | INCREMENT BY incrementValue 
   | MAXVALUE maxValue | NO MAXVALUE 
   | MINVALUE minValue | NO MINVALUE 
   | CYCLE | NO CYCLE 
}
```

dataType

If specified, the <span class="ItalicFont">dataType</span> must be an integer type (<span class="CodeFont">SMALLINT</span>, <span class="CodeFont">INT</span>, or <span class="CodeFont">BIGINT</span>). If not specified, the default data type is <span class="CodeFont">INT</span>.

startValue

If specified, this is a signed integer representing the first value returned by the sequence object. The <span class="CodeFont">START</span> value must be a value less than or equal to the maximum and greater than or equal to the minimum value of the sequence object.

The default start value for a new ascending sequence object is the minimum value. The default start value for a descending sequence objest is the maximum value.

incrementValue

If specifed, the <span class="CodeFont">incrementValue</span> is a non-zero signed integer value that fits in a <span class="ItalicFont">DataType</span> value.

If this is not specified, the <span class="CodeFont">INCREMENT</span> defaults to <span class="CodeFont">1</span>. If <span class="CodeFont">incrementValue</span> is positive, the sequence numbers get larger over time; if it is negative, the sequence numbers get smaller over time.

minValue

If specified, <span class="CodeFont">minValue</span> must be a signed integer that fits in a <span class="ItalicFont">DataType</span> value.

If <span class="CodeFont">minValue</span>is not specified, or if <span class="CodeFont">NO MINVALUE</span>is specified, then <span class="CodeFont">minValue</span>defaults to the smallest negative number that fits in a <span class="ItalicFont">DataType</span> value.

maxValue

If specified, <span class="CodeFont">maxValue</span> must be a signed integer that fits in a <span class="ItalicFont">DataType</span> value.

If <span class="CodeFont">maxValue</span>is not specified, or if <span class="CodeFont">NO MAXVALUE</span>is specified, then <span class="CodeFont">maxValue</span>defaults to the largest positive number that fits in a <span class="ItalicFont">DataType</span> value.

Note that the <span class="CodeFont">maxValue</span> must be greater than the <span class="CodeFont">minValue</span>.

CYCLE

The <span class="CodeFont">CYCLE</span> clause controls what happens when the sequence generator exhausts its range and wraps around.

If <span class="CodeFont">CYCLE</span> is specified, the wraparound behavior is to reinitialize the sequence generator to its <span class="CodeFont">START</span> value.

If <span class="CodeFont">NO CYCLE</span> is specified, Splice Machine throws an exception when the generator wraps around. The default behavior is <span class="CodeFont">NO CYCLE</span>.

To retrieve the next value from a sequence generator, use a [<span class="CodeFont">NEXT VALUE FOR</span> expression](../Expressions/NextValueFor.html).

Usage Privileges

The owner of the schema where the sequence generator lives automatically gains the <span class="CodeFont">USAGE</span> privilege on the sequence generator, and can grant this privilege to other users and roles. Only the database owner and the owner of the sequence generator can grant these <span class="CodeFont">USAGE</span> privileges. The <span class="CodeFont">USAGE</span> privilege cannot be revoked from the schema owner. See [<span class="CodeFont">GRANT statement</span>](Grant.html) and [<span class="CodeFont">REVOKE statement</span>](Revoke.html) for more information.

Performance

To boost performance and concurrency, Splice Machine pre-allocates ranges of upcoming values for sequences. The lengths of these ranges can be configured by adjusting the value of the derby.language.sequence.preallocator property.

Examples

The following statement creates a sequence generator of type <span class="CodeFont">INT</span>, with a start value of <span class="CodeFont">-2147483648</span> (the smallest <span class="CodeFont">INT</span> value). The value increases by <span class="CodeFont">1</span>, and the last legal value is the largest possible <span class="CodeFont">INT</span>. If <span class="CodeFont">NEXT VALUE FOR</span> is invoked on the generator after it reaches its maximum value, Splice Machine throws an exception.

``` Example
splice> CREATE SEQUENCE order_id;
0 rows inserted/updated/deleted
```

This example creates a player ID sequence that starts with the integer value <span class="CodeFont">100</span>:

``` Example
splice> CREATE SEQUENCE PlayerID_seq 
   START WITH 100;
0 rows inserted/updated/deleted
```

The following statement creates a sequence of type <span class="CodeFont">BIGINT</span> with a start value of <span class="CodeFont">3,000,000,000</span>. The value increases by <span class="CodeFont">1</span>, and the last legal value is the largest possible <span class="CodeFont">BIGINT</span>. If <span class="CodeFont">NEXT VALUE FOR</span> is invoked on the generator after it reaches its maximum value, Splice Machine throws an exception.

``` Example
splice> CREATE SEQUENCE order_entry_id
   AS BIGINT
   START WITH 3000000000;
0 rows inserted/updated/deleted
```

See Also

-   <span class="CodeFont">[DROP SEQUENCE](DropSequence.html)</span> statement
-   [<span class="CodeFont">GRANT</span>](Grant.html) statement
-   [<span class="CodeFont">Next Value For</span>](../Expressions/NextValueFor.html) expression
-   [<span class="CodeFont">REVOKE</span>](Revoke.html) statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   [SQL Identifier](../Identifiers/Intro.Identifiers.html)

 


