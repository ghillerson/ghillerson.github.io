[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateRole.html)

<a href="" id="Statements.CreateRole"></a>[]()CREATE ROLE
=========================================================

The <span class="CodeFont">CREATE ROLE</span> statement allows you to create an SQL role. Only the database owner can create a role.

Syntax

``` FcnSyntax
CREATE ROLE roleName
```

roleName

The name of an SQL role.

Using

Before you issue a <span class="CodeFont">CREATE ROLE</span> statement, verify that the <span class="ItalicFont">derby.database.sqlAuthorization</span> property is set to TRUE. The <span class="ItalicFont">derby.database.sqlAuthorization</span> property enables SQL authorization mode.

You cannot create a role name if there is already a user by that name. An attempt to create a role name that conflicts with an existing user name raises the <span class="ItalicFont">SQLException</span> X0Y68. If user names are not controlled by the database owner (or administrator), it may be a good idea to use a naming convention for roles to reduce the possibility of collision with user names.

Splice Machine tries to avoid name collision between user names and role names, but this is not always possible, because Splice Machine has a pluggable authorization architecture. For example, an externally defined user may exist who has never yet connected to the database, created any schema objects, or been granted any privileges. If Splice Machine knows about a user name, it will forbid creating a role with that name. Correspondingly, a user who has the same name as a role will not be allowed to connect. Splice Machine built-in users are checked for collision when a role is created.

A role name cannot start with the prefix <span class="CodeFont">SYS</span> (after case normalization). The purpose of this restriction is to reserve a name space for system-defined roles at a later point. Use of the prefix <span class="CodeFont">SYS</span> raises the <span class="ItalicFont">SQLException</span> 4293A.

You cannot create a role with the name PUBLIC (after case normalization). PUBLIC is a reserved authorization identifier. An attempt to create a role with the name PUBLIC raises <span class="ItalicFont">SQLException</span> 4251B.

Examples

Creating a Role

Here's a simple example of creating a role:

``` Example
splice> CREATE ROLE statsEditor_role;
0 rows inserted/updated/deleted
```

Examples of Invalid Role Names

Here are several examples of attempts to create a role using names that are reserved and cannot be used as role names. Each of these generates an error:

``` Example
splice> CREATE ROLE public;
splice> CREATE ROLE "PUBLIC";
splice> CREATE ROLE sysrole;
```

See Also

-   [<span class="CodeFont">DROP\_ROLE</span>](DropRole.html) statement
-   [<span class="CodeFont">GRANT</span>](Grant.html) statement
-   [<span class="CodeFont">REVOKE</span>](Revoke.html) statement
-   [RoleName](../Identifiers/IdentifierTypes.html#RoleName)
-   [<span class="CodeFont">SET ROLE</span>](SetRole.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table

 


