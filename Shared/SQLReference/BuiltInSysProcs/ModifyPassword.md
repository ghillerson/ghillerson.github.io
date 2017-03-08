[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/ModifyPassword.html)

<a href="" id="BuiltInSysProcs.ModifyPassword"></a>[]()SYSCS\_UTIL.SYSCS\_MODIFY\_PASSWORD
==========================================================================================

The SYSCS\_UTIL.SYSCS\_MODIFY\_PASSWORD system procedure is called by a user to change that user's own password.

This procedure is used in conjunction with NATIVE authentication.

The <span class="CodeFont">derby.authentication.native.passwordLifetimeMillis</span> property sets the password expiration time, and the <span class="CodeFont">derby.authentication.native.passwordLifetimeThreshold</span> property sets the time when a user is warned that the password will expire.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_MODIFY_PASSWORD(IN password VARCHAR(32672))
```

password

A case-sensitive password.

Results

This procedure does not return a result.

Execute Privileges

Any user can execute this procedure.

JDBC example

``` Example
CallableStatement cs = conn.prepareCall(
  "CALL SYSCS_UTIL.SYSCS_MODIFY_PASSWORD('baseball!')");
  cs.execute();
  cs.close();
```

SQL Example

The following example sets the current user's password to <span class="CodeFont">baseball!</span>:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_MODIFY_PASSWORD('baseball!');
Statement executed
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESET\_PASSWORD</span>](ResetPassword.html)

 


