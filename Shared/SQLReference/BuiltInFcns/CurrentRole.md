[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentRole.html)

<a href="" id="BuiltInFcns.CurrentRole"></a>[]()CURRENT\_ROLE
=============================================================

<span class="CodeFont">CURRENT\_ROLE</span> returns the authorization identifier of the current role. If there is no current role, it returns <span class="CodeFont">NULL</span>.

This function returns a string of up to <span class="CodeFont">258</span> characters. This is twice the length of an identifier <span class="CodeFont">(128\*2) + 2</span>, to allow for quoting.

Syntax

``` FcnSyntax
CURRENT_ROLE
```

Example

``` Example
splice> VALUES CURRENT_ROLE;
```

See Also

-   [<span class="CodeFont">CREATE\_ROLE</span>](../Statements/CreateRole.html) statement
-   [<span class="CodeFont">DROP\_ROLE</span>](../Statements/DropRole.html) statement
-   [<span class="CodeFont">GRANT</span>](../Statements/Grant.html) statement
-   [<span class="CodeFont">REVOKE</span>](../Statements/Revoke.html) statement
-   [<span class="CodeFont">SET ROLE</span>](../Statements/SetRole.html) statement
-   [<span class="CodeFont">SYSROLES</span>](../SystemTables/SysRoles.html) system table

 


