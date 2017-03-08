[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Grant.html)

<a href="" id="Statements.Grant"></a>[]()GRANT
==============================================

Use the <span class="CodeFont">GRANT</span> statement to give privileges to a specific user or role, or to all users, to perform actions on database objects. You can also use the <span class="CodeFont">GRANT</span> statement to grant a role to a user, to <span class="CodeFont">PUBLIC</span>, or to another role.

The syntax that you use for the <span class="CodeFont">GRANT</span> statement depends on whether you are granting privileges to a schema object or granting a role.

Syntax for Schemas

``` FcnSyntax
GRANT ALL PRIVILEGES | schema-privilege {, schema-privilege }*
   ON [SCHEMA] schema-Name 
   TO grantees
```

schema-privilege

<span class="CodeFont">DELETE |
INSERT |
REFERENCES \[( column-identifier {, column-identifier}\* )\] |
SELECT \[( column-identifier {, column-identifier}\* )\] |</span><span class="CodeFont">TRIGGER |</span><span class="CodeFont">
UPDATE \[( column-identifier {, column-identifier}\* )\]</span>

See the [Privilege Types](#PrivilegeTypes) section below for more information.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: Column-level privileges are available only with a Splice Machine Enterprise license.</span>

You cannot grant or revoke privileges at the <span class="CodeFont">column-identifier</span> level with the Community version of Splice Machine.

To obtain a license for the Splice Machine Enterprise Edition, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

schema-Name

The name of the schema to which you are granting access.

grantees

The user(s) or role(s) to whom you are granting access. See the [About Grantees](#AboutGrantees) section below for more information.

NOTES:

-   When you drop a schema from your database, all privileges associated with the schema are removed.
-   Table-level privileges override schema-level privileges.

Syntax for Tables

``` FcnSyntax
GRANT ALL PRIVILEGES | table-privilege {, table-privilege }*
   ON [TABLE] { table-Name | view-Name }
   TO grantees
```

table-privilege

<span class="CodeFont">DELETE |
INSERT |
REFERENCES \[( column-identifier {, column-identifier}\* )\] |
SELECT \[( column-identifier {, column-identifier}\* )\] |</span><span class="CodeFont">TRIGGER |</span><span class="CodeFont">
UPDATE \[( column-identifier {, column-identifier}\* )\]</span>

See the [Privilege Types](#PrivilegeTypes) section below for more information.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: Column-level privileges are available only with a Splice Machine Enterprise license.</span>

You cannot grant or revoke privileges at the <span class="CodeFont">column-identifier</span> level with the Community version of Splice Machine.

To obtain a license for the Splice Machine Enterprise Edition, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

table-Name

The name of the table to which you are granting access.

view-Name

The name of the view to which you are granting access.

schema-Name

The name of the schema to which you are granting access.

grantees

The user(s) or role(s) to whom you are granting access. See the [About Grantees](#AboutGrantees) section below for more information.

NOTES:

-   When you drop a table from your database, all privileges associated with the table are removed.
-   Table-level privileges override schema-level privileges.

Syntax for Routines

``` FcnSyntax
GRANT EXECUTE
   ON { FUNCTION | PROCEDURE } {function-name | procedure-name}
   TO grantees
```

function-name | procedure-name

The name of the function or procedure to which you are granting access.

grantees

The user(s) or role(s) to whom you are granting access. See the [About Grantees](#AboutGrantees) section below for more information.

Syntax for User-defined Types

``` FcnSyntax
GRANT USAGE
   ON TYPE [ schemaName. ] SQL Identifier
   TO grantees
```

\[schema-name.\] SQL Identifier

The type name is composed of an optional <span class="ItalicFont">schemaName</span> and a <span class="ItalicFont">SQL Identifier</span>. If a <span class="ItalicFont">schemaName</span> is not provided, the current schema is the default schema. If a qualified UDT name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

grantees

The user(s) or role(s) to whom you are granting access. See the [About Grantees](#AboutGrantees) section below for more information.

Syntax for Roles

``` FcnSyntax
GRANT roleName [ {, roleName }* ]
   TO grantees
```

roleName

The name to the role(s) to which you are granting access.

grantees

The user(s) or role(s) to whom you are granting access. See the [About Grantees](#AboutGrantees) section below for more information.

Before you can grant a role to a user or to another role, you must create the role using the [<span class="CodeFont">CREATE ROLE</span> statement](CreateRole.html). Only the database owner can grant a role.

A role A <span class="ItalicFont">contains</span> another role B if role B is granted to role A, or is contained in a role C granted to role A. Privileges granted to a contained role are inherited by the containing roles. So the set of privileges identified by role A is the union of the privileges granted to role A and the privileges granted to any contained roles of role A.

[]()About Grantees

A grantee can be one or more specific users, one or more specific roles, or all users (<span class="CodeFont">PUBLIC</span>). Either the object owner or the database owner can grant privileges to a user or to a role. Only the database owner can grant a role to a user or to another role.

Here's the syntax:

``` FcnSyntax
{     AuthorizationIdentifier | roleName | PUBLIC } 
   [, { AuthorizationIdentifier | roleName | PUBLIC } ] *
```

AuthorizationIdentifier

An expression.

roleName

The name of the role.

Either the object owner or the database owner can grant privileges to a user or to a role. Only the database owner can grant a role to a user or to another role.

<span class="CodeFont">PUBLIC</span>

Use the keyword <span class="CodeFont">PUBLIC</span> to specify all users.

When <span class="CodeFont">PUBLIC</span> is specified, the privileges or roles affect all current and future users.

The privileges granted to <span class="CodeFont">PUBLIC</span> and to individual users or roles are independent privileges. For example, a <span class="CodeFont">SELECT</span> privilege on table t is granted to both <span class="CodeFont">PUBLIC</span> and to the authorization ID harry. If the <span class="CodeFont">SELECT</span> privilege is later revoked from the authorization ID harry, Harry will still be able to access the table t through the <span class="CodeFont">PUBLIC</span> privilege.

[]()Privilege Types

| Privilege Type | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ALL PRIVILEGES | To grant all of the privileges to the user or role for the specified table. You can also grant one or more table privileges by specifying a privilege-list.                                                                                                                                                                                                                                                                                               |
| DELETE         | To grant permission to delete rows from the specified table.                                                                                                                                                                                                                                                                                                                                                                                              |
| INSERT         | To grant permission to insert rows into the specified table.                                                                                                                                                                                                                                                                                                                                                                                              |
| REFERENCES     | To grant permission to create a foreign key reference to the specified table. If a column list is pecified with the <span class="CodeFont">REFERENCES</span> privilege, the permission is valid on only the foreign key reference to the specified columns.                                                                                                                                                                                               |
| SELECT         | To grant permission to perform [<span class="CodeFont">SELECT</span> statements](Select.html) or <span class="ItalicFont">[SelectExpressions](../Expressions/Select.html)</span> on a table or view. If a column list is specified with the <span class="CodeFont">SELECT</span> privilege, the permission is valid on only those columns. If no column list is specified, then the privilege is valid on all of the columns in the table.                
                  For queries that do not select a specific column from the tables involved in a <span class="CodeFont">SELECT</span> statement or <span class="ItalicFont">SelectExpression</span> (for example, queries that use COUNT(\*)), the user must have at least one column-level <span class="CodeFont">SELECT</span> privilege or table-level <span class="CodeFont">SELECT</span> privilege.                                                                    |
| TRIGGER        | To grant permission to create a trigger on the specified table.                                                                                                                                                                                                                                                                                                                                                                                           |
| UPDATE         | To grant permission to use the <span class="CodeFont">[UPDATE](UpdateTable.html)</span> statement on the specified table. If a column list is specified, the permission applies only to the specified columns. To update a row using a statement that includes a <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause, you must have the <span class="CodeFont">SELECT</span> privilege on the columns in the row that you want to update. |

Usage Notes

The following types of privileges can be granted:

-   Delete data from a specific table.
-   Insert data into a specific table.
-   Create a foreign key reference to the named table or to a subset of columns from a table.
-   Select data from a table, view, or a subset of columns in a table.
-   Create a trigger on a table.
-   Update data in a table or in a subset of columns in a table.
-   Run a specified function or procedure.
-   Use a user-defined type.

Before you issue a <span class="CodeFont">GRANT</span> statement, check that the derby.database.sqlAuthorization property is set to true. The derby.database.sqlAuthorization property enables the SQL Authorization mode.

You can grant privileges on an object if you are the owner of the object or the database owner. See documentation for the <span class="CodeFont">[CREATE](Intro.DDLCreateStatements.html)</span> statements for more information.

Examples

Granting Privileges to Users

To grant the <span class="CodeFont">SELECT</span> privilege on the schema SpliceBBall to the authorization IDs Bill and Joan, use the following syntax:

``` Example
splice> GRANT SELECT ON SCHEMA SpliceBBall TO Bill, Joan;
0 rows inserted/updated/deleted
```

To grant the <span class="CodeFont">SELECT</span> privilege on table Salaries to the authorization IDs Bill and Joan, use the following syntax:

``` Example
splice> GRANT SELECT ON TABLE Salaries TO Bill, Joan;
0 rows inserted/updated/deleted
```

To grant the <span class="CodeFont">UPDATE</span> and <span class="CodeFont">TRIGGER</span> privileges on table Salaries to the authorization IDs Joe and Anita, use the following syntax:

``` Example
splice> GRANT UPDATE, TRIGGER ON TABLE Salaries TO Joe, Anita;
0 rows inserted/updated/deleted
```

To grant the <span class="CodeFont">SELECT</span> privilege on table <span class="CodeFont">Hitting</span> in the <span class="CodeFont">Baseball\_stats</span> schema to all users, use the following syntax:

``` Example
splice> GRANT SELECT ON TABLE Baseball_Stats.Hitting to PUBLIC;
0 rows inserted/updated/deleted
```

To grant the <span class="CodeFont">EXECUTE</span> privilege on procedure ComputeValue to the authorization ID george, use the following syntax:

``` Example
splice> GRANT EXECUTE ON PROCEDURE ComputeValue TO george;
0 rows inserted/updated/deleted
```

Granting Roles to Users

To grant the role purchases\_reader\_role to the authorization IDs george and maria, use the following syntax:

``` Example
splice> GRANT purchases_reader_role TO george,maria;
0 rows inserted/updated/deleted
```

Granting Privileges to Roles

To grant the <span class="CodeFont">SELECT</span> privilege on schema SpliceBBall to the role purchases\_reader\_role, use the following syntax:

``` Example
splice> GRANT SELECT ON SCHEMA SpliceBBall TO purchases_reader_role;
0 rows inserted/updated/deleted
```

To grant the <span class="CodeFont">SELECT</span> privilege on table t to the role purchases\_reader\_role, use the following syntax:

``` Example
splice> GRANT SELECT ON TABLE t TO purchases_reader_role;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CREATE ROLE</span>](CreateRole.html) statement
-   [<span class="CodeFont">CREATE TRIGGER</span>](CreateTrigger.html) statement
-   [<span class="CodeFont">DROP\_ROLE</span>](DropRole.html) statement
-   [<span class="CodeFont">REVOKE</span>](Revoke.html) statement
-   [<span class="CodeFont">RoleName</span>](../Identifiers/IdentifierTypes.html#RoleName)
-   [<span class="CodeFont">SET ROLE</span>](SetRole.html) statement
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">SELECT</span>](Select.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table
-   [<span class="CodeFont">UPDATE</span>](UpdateTable.html) statement
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


