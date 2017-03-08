[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropSequence.html)

<a href="" id="Statements.DropSequence"></a>[]()DROP SEQUENCE
=============================================================

The <span class="CodeFont">DROP SEQUENCE</span> statement removes a sequence generator that was created using a [<span class="CodeFont">CREATE SEQUENCE</span> statement](CreateSequence.html).

Syntax

``` FcnSyntax
DROP SEQUENCE [ schemaName. ] SQL Identifier RESTRICT
```

schemaName

The name of the schema to which this sequence belongs. If you do not specify a schema name, the current schema is assumed.

You cannot use a schema name that begins with the <span class="CodeFont">SYS.</span> prefix.

SQL Identifier

The name of the sequence.

RESTRICT

This is <span class="BoldFont">required</span>. It specifies that if a trigger or view references the sequence generator, Splice Machine will throw an exception.

Usage

Dropping a sequence generator implicitly drops all <span class="CodeFont">USAGE</span> privileges that reference it.

Example

``` Example
splice> DROP SEQUENCE PLAYERID_SEQ RESTRICT;
0 rows inserted/updated/deleted
```

See Also

-   <span class="CodeFont">[CREATE SEQUENCE](CreateSequence.html)</span> statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)

 


