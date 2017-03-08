[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Revoke.html)

<a href="" id="Statements.Revoke"></a>[]()REVOKE
================================================

Use the <span class="CodeFont">REVOKE</span> statement to remove privileges from a specific user or role, or from all users, to perform actions on database objects. You can also use the <span class="CodeFont">REVOKE</span> statement to revoke a role from a user, from <span class="CodeFont">PUBLIC</span>, or from another role.

The syntax that you use for the <span class="CodeFont">REVOKE</span> statement depends on whether you are revoking privileges to a schema object or revoking a role.

Syntax for SCHEMA

``` FcnSyntax
REVOKE privilege-type 
   ON [ SCHEMA ] S 
   FROM grantees
```

privilege-type

<span class="CodeFont">DELETE |
INSERT |
REFERENCES \[( column-identifier {, column-identifier}\* )\] |
SELECT \[( column-identifier {, column-identifier}\* )\] |
</span><span class="CodeFont">TRIGGER |
</span><span class="CodeFont">UPDATE \[( column-identifier {, column-identifier}\* )\]</span>

See the [Privilege Types](#PrivilegeTypes) section below for more information.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: Column-level privileges are available only with a Splice Machine Enterprise license.</span>

You cannot grant or revoke privileges at the <span class="CodeFont">column-identifier</span> level with the Community version of Splice Machine.

To obtain a license for the Splice Machine Enterprise Edition, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

schema-Name

The name of the schemafor which you are revoking access.

grantees

The user(s) or role(s) for whom you are revoking access. See the [About Grantees](#AboutGrantees) section below for more information.

Syntax for Tables

``` FcnSyntax
REVOKE privilege-type 
   ON [ TABLE ] { table-Name | view-Name } 
   FROM grantees
```

privilege-type

<span class="CodeFont">DELETE |
INSERT |
REFERENCES \[( column-identifier {, column-identifier}\* )\] |
SELECT \[( column-identifier {, column-identifier}\* )\] |
</span><span class="CodeFont">TRIGGER |
</span><span class="CodeFont">UPDATE \[( column-identifier {, column-identifier}\* )\]</span>

See the [Privilege Types](#PrivilegeTypes) section below for more information.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: Column-level privileges are available only with a Splice Machine Enterprise license.</span>

You cannot grant or revoke privileges at the <span class="CodeFont">column-identifier</span> level with the Community version of Splice Machine.

To obtain a license for the Splice Machine Enterprise Edition, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

table-Name

The name of the table for which you are revoking access.

view-Name

The name of the view for which you are revoking access.

grantees

The user(s) or role(s) for whom you are revoking access. See the [About Grantees](#AboutGrantees) section below for more information.

Syntax for Routines

``` FcnSyntax
REVOKE EXECUTE ON { FUNCTION | PROCEDURE } 
    {function-name | procedure-name}
 TO grantees RESTRICT
```

function-name | procedure-name

The name of the function or procedure for which you are revoking access.

grantees

The user(s) or role(s) for whom you are revoking access. See the [About Grantees](#AboutGrantees) section below for more information.

RESTRICT

You <span class="BoldFont">must</span> use this clause when revoking access for routines.

The <span class="CodeFont">RESTRICT</span> clause specifies that the <span class="CodeFont">EXECUTE</span> privilege cannot be revoked if the specified routine is used in a view, trigger, or constraint, and the privilege is being revoked from the owner of the view, trigger, or constraint.

Syntax for User-defined types

``` FcnSyntax
REVOKE USAGE 
   ON TYPE  [ schemaName. ] SQL Identifier 
   FROM grantees RESTRICT
```

\[schema-name.\] SQL Identifier

The user-defined type (UDT) name is composed of an optional <span class="ItalicFont">schemaName</span> and a <span class="ItalicFont">SQL Identifier</span>. If a <span class="ItalicFont">schemaName</span> is not provided, the current schema is the default schema. If a qualified UDT name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

grantees

The user(s) or role(s) for whom you are revoking access. See the [About Grantees](#AboutGrantees) section below for more information.

RESTRICT

You <span class="BoldFont">must</span> use this clause when revoking access for user-defined types.

The <span class="CodeFont">RESTRICT</span> clause specifies that the <span class="CodeFont">EXECUTE</span> privilege cannot be revoked if the specified UDT is used in a view, trigger, or constraint, and the privilege is being revoked from the owner of the view, trigger, or constraint.

Syntax for Roles

``` FcnSyntax
REVOKE roleName [ {, roleName }* ] 
   FROM grantees
```

roleName

The name to the role(s) for which you are revoking access.

grantees

The user(s) or role(s) for whom you are revoking access. See the [About Grantees](#AboutGrantees) section below for more information.

Only the database owner can revoke a role.

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

The privileges granted to <span class="CodeFont">PUBLIC</span> and to individual users or roles are independent privileges. For example, a <span class="CodeFont">SELECT</span> privilege on table t is granted to both <span class="CodeFont">PUBLIC</span> and to the authorization ID harry. If the <span class="CodeFont">SELECT</span> privilege is later revoked from the authorization ID harry, Harry will still be able to access the table t through the <span class="CodeFont">PUBLIC</span> privilege..

[]()Privilege Types

| Privilege Type | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ALL PRIVILEGES | To revoke all of the privileges to the user or role for the specified table. You can also grant one or more table privileges by specifying a privilege-list.                                                                                                                                                                                                                                                                                               |
| DELETE         | To revoke permission to delete rows from the specified table.                                                                                                                                                                                                                                                                                                                                                                                              |
| INSERT         | To revoke permission to insert rows into the specified table.                                                                                                                                                                                                                                                                                                                                                                                              |
| REFERENCES     | To revoke permission to create a foreign key reference to the specified table. If a column list is pecified with the <span class="CodeFont">REFERENCES</span> privilege, the permission is valid on only the foreign key reference to the specified columns.                                                                                                                                                                                               |
| SELECT         | To revoke permission to perform [<span class="CodeFont">SELECT</span> statements](Select.html) or <span class="ItalicFont">[SelectExpressions](../Expressions/Select.html)</span> on a table or view. If a column list is specified with the <span class="CodeFont">SELECT</span> privilege, the permission is valid on only those columns. If no column list is specified, then the privilege is valid on all of the columns in the table.                
                  For queries that do not select a specific column from the tables involved in a <span class="CodeFont">SELECT</span> statement or <span class="ItalicFont">SelectExpression</span> (for example, queries that use COUNT(\*)), the user must have at least one column-level <span class="CodeFont">SELECT</span> privilege or table-level <span class="CodeFont">SELECT</span> privilege.                                                                     |
| TRIGGER        | To revoke permission to create a trigger on the specified table.                                                                                                                                                                                                                                                                                                                                                                                           |
| UPDATE         | To revoke permission to use the <span class="CodeFont">[UPDATE](UpdateTable.html)</span> statement on the specified table. If a column list is specified, the permission applies only to the specified columns. To update a row using a statement that includes a <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause, you must have the <span class="CodeFont">SELECT</span> privilege on the columns in the row that you want to update. |

Usage Notes

The following types of privileges can be revoked:

-   Delete data from a specific table.
-   Insert data into a specific table.
-   Create a foreign key reference to the named table or to a subset of columns from a table.
-   Select data from a table, view, or a subset of columns in a table.
-   Create a trigger on a table.
-   Update data in a table or in a subset of columns in a table.
-   Run a specified routine (function or procedure).
-   Use a user-defined type.

Before you issue a <span class="CodeFont">REVOKE</span> statement, check that the derby.database.sqlAuthorization property is set to true. The derby.database.sqlAuthorization property enables the SQL Authorization mode.

You can revoke privileges on an object if you are the owner of the object or the database owner. See the <span class="CodeFont">CREATE</span> statement for the database object that you want To revoke privileges on for more information.

You can revoke privileges for an object if you are the owner of the object or the database owner.

Prepared statements and open result sets

Checking for privileges happens at statement execution time, so prepared statements are still usable after a revoke action. If sufficient privileges are still available for the session, prepared statements will be executed, and for queries, a result set will be returned.

Once a result set has been returned to the application (by executing a prepared statement or by direct execution), it will remain accessible even if privileges or roles are revoked in a way that would cause another execution of the same statement to fail.

Cascading object dependencies

For views, triggers, and constraints, if the privilege on which the object depends on is revoked, the object is automatically dropped. Splice Machine does not try to determine if you have other privileges that can replace the privileges that are being revoked.

Limitations

The following limitations apply to the REVOKE statement:

Table-level privileges

All of the table-level privilege types for a specified grantee and table ID are stored in one row in the <span class="CodeFont">SYSTABLEPERMS</span> system table. For example, when user2 is granted the <span class="CodeFont">SELECT</span> and <span class="CodeFont">DELETE</span> privileges on table user1.t1, a row is added to the <span class="CodeFont">SYSTABLEPERMS</span> table. The <span class="CodeFont">GRANTEE</span> field contains user2 and the <span class="CodeFont">TABLEID</span> contains user1.t1. The <span class="CodeFont">SELECTPRIV</span> and <span class="CodeFont">DELETEPRIV</span> fields are set to Y. The remaining privilege type fields are set to N.

When a grantee creates an object that relies on one of the privilege types, Splice Machine engine tracks the dependency of the object on the specific row in the <span class="CodeFont">SYSTABLEPERMS</span> table. For example, user2 creates the view v1 by using the statement SELECT \* FROM user1.t1, the dependency manager tracks the dependency of view v1 on the row in <span class="CodeFont">SYSTABLEPERMS</span> for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>(user1.t1).

The dependency manager knows only that the view is dependent on a privilege type in that specific row, but does not track exactly which privilege type the view is dependent on.

When a <span class="CodeFont">REVOKE</span> statement for a table-level privilege is issued for a grantee and table ID, all of the objects that are dependent on the grantee and table ID are dropped. For example, if user1 revokes the <span class="CodeFont">DELETE</span> privilege on table t1 from user2, the row in <span class="CodeFont">SYSTABLEPERMS</span> for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>(user1.t1) is modified by the <span class="CodeFont">REVOKE</span> statement. The dependency manager sends a revoke invalidation message to the view user2.v1 and the view is dropped even though the view is not dependent on the <span class="CodeFont">DELETE</span> privilege for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>(user1.t1).

Column-level privileges

Only one type of privilege for a specified grantee and table ID are stored in one row in the <span class="CodeFont">SYSCOLPERMS</span> system table. For example, when user2 is granted the <span class="CodeFont">SELECT</span> privilege on table user1.t1 for columns c12 and c13, a row is added to the <span class="CodeFont">SYSCOLPERMS</span>. The <span class="CodeFont">GRANTEE</span> field contains user2, the <span class="CodeFont">TABLEID</span> contains user1.t1, the <span class="CodeFont">TYPE</span> field contains S, and the <span class="CodeFont">COLUMNS</span> field contains c12, c13.

When a grantee creates an object that relies on the privilege type and the subset of columns in a table ID, Splice Machine engine tracks the dependency of the object on the specific row in the <span class="CodeFont">SYSCOLPERMS</span> table. For example, user2 creates the view v1 by using the statement SELECT c11 FROM user1.t1, the dependency manager tracks the dependency of view v1 on the row in <span class="CodeFont">SYSCOLPERMS</span> for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>(user1.t1), <span class="CodeFont">TYPE</span>(s). The dependency manager knows that the view is dependent on the <span class="CodeFont">SELECT</span> privilege type, but does not track exactly which columns the view is dependent on.

When a <span class="CodeFont">REVOKE</span> statement for a column-level privilege is issued for a grantee, table ID, and type, all of the objects that are dependent on the grantee, table ID, and type are dropped. For example, if user1 revokes the <span class="CodeFont">SELECT</span> privilege on column c12 on table user1.t1 from user2, the row in <span class="CodeFont">SYSCOLPERMS</span> for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>( ser1.t1), <span class="CodeFont">TYPE</span>(s) is modified by the <span class="CodeFont">REVOKE</span> statement. The dependency manager sends a revoke invalidation message to the view user2.v1 and the view is dropped even though the view is not dependent on the column c12 for <span class="CodeFont">GRANTEE</span>(user2), <span class="CodeFont">TABLEID</span>(user1.t1), <span class="CodeFont">TYPE</span>(s).

Roles

Splice Machine tracks any dependencies on the definer's current role for views and constraints, constraints, and triggers. If privileges were obtainable only via the current role when the object in question was defined, that object depends on the current role. The object will be dropped if the role is revoked from the defining user or from <span class="CodeFont">PUBLIC</span>, as the case may be.

Also, if a contained role of the current role in such cases is revoked, dependent objects will be dropped. Note that dropping may be too pessimistic. This is because Splice Machine does not currently make an attempt to recheck if the necessary privileges are still available in such cases.

Revoke Examples

Revoking User Privileges

To revoke the <span class="CodeFont">SELECT</span> privilege on schema SpliceBBall from the authorization IDs Bill and Joan, use the following syntax:

``` Example
splice> REVOKE SELECT ON SCHEMA SpliceBBall FROM Bill, Joan;
0 rows inserted/updated/deleted
```

To revoke the <span class="CodeFont">SELECT</span> privilege on table Salaries from the authorization IDs Bill and Joan, use the following syntax:

``` Example
splice> REVOKE SELECT ON TABLE Salaries FROM Bill, Joan;
0 rows inserted/updated/deleted
```

To revoke the <span class="CodeFont">UPDATE</span> and <span class="CodeFont">TRIGGER</span> privileges on table Salaries from the authorization IDs Joe and Anita, use the following syntax:

``` Example
splice> REVOKE UPDATE, TRIGGER ON TABLE Salaries FROM Joe, Anita;
0 rows inserted/updated/deleted
```

To revoke the <span class="CodeFont">SELECT</span> privilege on table <span class="CodeFont">Hitting</span> in the <span class="CodeFont">Baseball\_stats</span> schema from all users, use the following syntax:

``` Example
splice> REVOKE SELECT ON TABLE Baseball_Stats.Hitting FROM PUBLIC;
0 rows inserted/updated/deleted
```

To revoke the <span class="CodeFont">EXECUTE</span> privilege on procedure ComputeValue from the authorization ID george, use the following syntax:

``` Example
splice> REVOKE EXECUTE ON PROCEDURE ComputeValue FROM george;
0 rows inserted/updated/deleted
```

Revoking User Roles

To revoke the role purchases\_reader\_role from the authorization IDs george and maria, use the following syntax:

``` Example
splice> REVOKE purchases_reader_role FROM george,maria;
0 rows inserted/updated/deleted
```

Revoking Role Privileges

To revoke the <span class="CodeFont">SELECT</span> privilege on schema SpliceBBall from the role purchases\_reader\_role, use the following syntax:

``` Example
splice> REVOKE SELECT ON SCHEMA SpliceBBall FROM purchases_reader_role;
0 rows inserted/updated/deleted
```

To revoke the <span class="CodeFont">SELECT</span> privilege on table t to the role purchases\_reader\_role, use the following syntax:

``` Example
splice> REVOKE SELECT ON TABLE t FROM purchases_reader_role;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CREATE ROLE</span>](CreateRole.html) statement
-   [<span class="CodeFont">DROP\_ROLE</span>](DropRole.html) statement
-   [<span class="CodeFont">GRANT</span>](Grant.html) statement
-   [<span class="CodeFont">RoleName</span>](../Identifiers/IdentifierTypes.html#RoleName)
-   [<span class="CodeFont">SET ROLE</span>](SetRole.html) statement
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">SELECT</span>](Select.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table
-   [<span class="CodeFont">UPDATE</span>](UpdateTable.html) statement
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


