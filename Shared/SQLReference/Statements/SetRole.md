[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/SetRole.html)

<a href="" id="Statements.SetRole"></a>[]()SET ROLE
===================================================

The <span class="CodeFont">SET ROLE</span> statement allows you to set the current role for the current SQL context of a session.

You can set a role only if the current user has been granted the role, or if the role has been granted to <span class="CodeFont">PUBLIC</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The <span class="CodeFont">SET ROLE</span> statement is not transactional; a rollback does not undo the effect of setting a role. If a transaction is in progress, an attempt to set a role results in an error.

Syntax

``` FcnSyntax
SET ROLE { roleName | 'string-constant' | ? | NONE }
```

roleName

The role you want set as the current role.

You can specify a <span class="ItalicFont">roleName</span> of <span class="CodeFont">NONE</span> to unset the current role.

If you specify the role as a string constant or as a dynamic parameter specification (?), any leading and trailing blanks are trimmed from the string before attempting to use the remaining (sub)string as a <span class="ItalicFont">roleName</span>. The dynamic parameter specification can be used in prepared statements, so the <span class="CodeFont">SET ROLE</span> statement can be prepared once and then executed with different role values. You cannot specify <span class="CodeFont">NONE</span> as a dynamic parameter.

Usage Notes

Setting a role identifies a set of privileges that is a union of the following:

-   The privileges granted to that role
-   The union of privileges of roles contained in that role (for a definition of role containment, see "Syntax for roles" in [<span class="CodeFont">GRANT</span> statement](Grant.html))

In a session, the <span class="ItalicFont">current privileges</span> define what the session is allowed to access. The <span class="ItalicFont">current privileges</span> are the union of the following:

-   The privileges granted to the current user
-   The privileges granted to <span class="CodeFont">PUBLIC</span>
-   The privileges identified by the current role, if set

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> You can find the available role names in the <span class="CodeFont">[SYS.SYSROLES](../SystemTables/SysRoles.html)</span> system table.

SQL Example

This examples set the role of the current user to <span class="CodeFont">reader\_role</span>:

``` Example
splice> SET ROLE reader_role;
0 rows inserted/updated/deleted
```

JDBC Example

This examples set the role of the current user to <span class="CodeFont">reader\_role</span>:

``` Example
stmt.execute("SET ROLE admin");      -- case normal form: ADMIN
stmt.execute("SET ROLE \"admin\"");  -- case normal form: admin
stmt.execute("SET ROLE none");       -- special case

PreparedStatement ps = conn.prepareStatement("SET ROLE ?");
ps.setString(1, "  admin ");         -- on execute: case normal form: ADMIN
ps.setString(1, "\"admin\"");        -- on execute: case normal form: admin
ps.setString(1, "none");             -- on execute: syntax error
ps.setString(1, "\"none\"");         -- on execute: case normal form: none
```

See Also

-   [<span class="CodeFont">CREATE ROLE</span>](CreateRole.html) statement
-   [<span class="CodeFont">DROP\_ROLE</span>](DropRole.html) statement
-   [<span class="CodeFont">GRANT</span>](Grant.html) statement
-   [<span class="CodeFont">REVOKE</span>](Revoke.html) statement
-   [RoleName](../Identifiers/IdentifierTypes.html#RoleName)
-   [<span class="CodeFont">SET ROLE</span>](#) statement
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">SELECT</span>](Select.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table
-   [<span class="CodeFont">UPDATE</span>](UpdateTable.html) statement
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


