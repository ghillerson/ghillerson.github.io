[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropRole.html)

<a href="" id="Statements.DropRole"></a>[]()DROP ROLE
=====================================================

The <span class="CodeFont">DROP ROLE</span> statement allows you to drop a role from your database.

Syntax

``` FcnSyntax
DROP ROLE roleName
```

roleName

The name of the role that you want to drop from your database.

Usage

Dropping a role has the effect of removing the role from the database dictionary. This means that no session user can henceforth set that role (see [<span class="CodeFont">SET ROLE</span> statement](SetRole.html)), and any existing sessions that have that role as the current role (see the [<span class="CodeFont">CURRENT\_ROLE</span> function](../BuiltInFcns/CurrentRole.html)) will now have a <span class="CodeFont">NULL CURRENT\_ROLE</span>.

Dropping a role also has the effect of revoking that role from any user and role it has been granted to. See the [<span class="CodeFont">REVOKE</span> statement](Revoke.html) for information on how revoking a role may impact any dependent objects.

Example

``` Example
splice> DROP ROLE statsEditor_role;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CREATE\_ROLE</span>](CreateRole.html) statement
-   [<span class="CodeFont">GRANT</span>](Grant.html) statement
-   [<span class="CodeFont">REVOKE</span>](Revoke.html) statement
-   [<span class="CodeFont">SET ROLE</span>](SetRole.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table

 


