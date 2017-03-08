[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropSchema.html)

<a href="" id="Statements.DropSchema"></a>[]()DROP SCHEMA
=========================================================

The <span class="CodeFont">DROP SCHEMA</span> statement drops a schema. The target schema must be empty for the drop to succeed.

Neither the <span class="ItalicFont">SPLICE</span> schema (the default user schema) nor the <span class="ItalicFont">SYS</span> schema can be dropped.

Syntax

``` FcnSyntax
DROP SCHEMA schemaName RESTRICT
```

schema

The name of the schema that you want to drop from your database.

RESTRICT

This is <span class="BoldFont">required</span>. It enforces the rule that the schema cannot be deleted from the database if there are any objects defined in the schema.

Example

``` Example
splice> DROP SCHEMA Baseball_Stats RESTRICT;
0 rows inserted/updated/deleted
```

See Also

-   <span class="CodeFont">[CREATE SCHEMA](CreateSchema.html)</span> statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   <span class="CodeFont">[SET SCHEMA](SetSchema.html)</span> statement

 


