[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/SetSchema.html)

<a href="" id="Statements.SetSchema"></a>[]()SET SCHEMA
=======================================================

The <span class="CodeFont">SET SCHEMA</span> statement sets the default schema for a connection's session to the designated schema. The default schema is used as the target schema for all statements issued from the connection that do not explicitly specify a schema name.

The target schema must exist for the <span class="CodeFont">SET SCHEMA</span> statement to succeed. If the schema doesn't exist an error is returned. See the [<span class="CodeFont">CREATE SCHEMA</span> statement](CreateSchema.html)

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The <span class="CodeFont">SET SCHEMA</span> statement is not transactional: if the <span class="CodeFont">SET SCHEMA</span> statement is part of a transaction that is rolled back, the schema change remains in effect.

Syntax

``` FcnSyntax
SET [CURRENT] SCHEMA [=] schemaName
```

schemaName

The name of the schema; this name is not case sensitive.

Examples

These examples are equivalent:

``` Example
splice> SET SCHEMA BASEBALL; 
0 rows inserted/updated/deleted

splice> SET SCHEMA Baseball;
0 rows inserted/updated/deleted

splice> SET CURRENT SCHEMA BaseBall;
0 rows inserted/updated/deleted

splice> SET CURRENT SQLID BASEBALL;
0 rows inserted/updated/deleted

splice> SET SCHEMA "BASEBALL";
0 rows inserted/updated/deleted

splice> SET SCHEMA 'BASEBALL'
0 rows inserted/updated/deleted
```

These fail because of case sensitivity:

``` Example
splice> SET SCHEMA "Baseball";
ERROR 42Y07: Schema 'Baseball' does not exist

splice> SET SCHEMA 'BaseBall';
ERROR 42Y07: Schema 'BaseBall' does not exist
```

Here's an example using a prepared statement:

``` Example
PreparedStatement ps = conn.PrepareStatement("set schema ?");
ps.setString(1,"HOTEL");
ps.executeUpdate();
  ... these work:
ps.setString(1,"SPLICE");

ps.executeUpdate();
ps.setString(1,"splice");       //error - string is case sensitive
    // no app will be found 
 ps.setNull(1, Types.VARCHAR); //error - null is not allowed
```

See Also

-   <span class="CodeFont">[CREATE SCHEMA](CreateSchema.html)</span> statement
-   <span class="CodeFont">[DROP SCHEMA](DropSchema.html)</span> statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)

 


