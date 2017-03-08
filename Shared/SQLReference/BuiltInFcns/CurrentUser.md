[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentUser.html)

<a href="" id="BuiltInFcns.CurrentUser"></a>[]()CURRENT\_USER
=============================================================

When used outside stored routines, [<span class="CodeFont">CURRENT\_USER</span>](#), [<span class="CodeFont">USER</span>](User.html), and [<span class="CodeFont">SESSION\_USER</span>](SessionUser.html) all return the authorization identifier of the user who created the SQL session.

<span class="CodeFont">SESSION\_USER</span> also always returns this value when used within stored routines.

If used within a stored routine created with <span class="CodeFont">EXTERNAL SECURITY DEFINER</span>, however, <span class="CodeFont">CURRENT\_USER</span> and <span class="CodeFont">[USER](User.html)</span> return the authorization identifier of the user that owns the schema of the routine. This is usually the creating user, although the database owner could be the creator as well.

For information about definer's and invoker's rights, see [<span class="CodeFont">CREATE PROCEDURE</span> statement](../Statements/CreateProcedure.html) or [<span class="CodeFont">CREATE FUNCTION</span> statement](../Statements/CreateFunction.html).

Each of these functions returns a string of up to 128 characters.

Syntax

``` FcnSyntax
CURRENT_USER
```

Example

``` Example
splice> VALUES CURRENT_USER;
1
--------------------------------------------------------------------
SPLICE

1 row selected
```

See Also

-   [<span class="CodeFont">USER</span>](User.html) function
-   [<span class="CodeFont">SESSION\_USER</span>](SessionUser.html) function
-   [<span class="CodeFont">CREATE\_FUNCTION</span>](../Statements/CreateFunction.html) statement
-   [<span class="CodeFont">CREATE\_PROCEDURE</span>](../Statements/CreateProcedure.html) statement

 


