[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/ResetPassword.html)

<a href="" id="BuiltInSysProcs.ResetPassword"></a>[]()SYSCS\_UTIL.SYSCS\_RESET\_PASSWORD
========================================================================================

The SYSCS\_UTIL.SYSCS\_RESET\_PASSWORD system procedure resets a password for a user whose password has expired or has been forgotten.

This procedure is used in conjunction with NATIVE authentication.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_RESET_PASSWORD(IN userName VARCHAR(128),
                         IN password VARCHAR(32672))
```

userName

A user name that is case-sensitive if you place the name string in double quotes. This user name is an authorization identifier..

password

A case-sensitive password.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC example

Reset the password of a user named FRED:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_RESET_PASSWORD(?, ?)");
  cs.setString(1, "fred");
  cs.setString(2, "temppassword");
  cs.execute();
  cs.close();
```

Reset the password of a user named FreD:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_RESET_PASSWORD(?, ?)");
  cs.setString(1, "\"FreD\"");
  cs.setString(2, "temppassword");
  cs.execute();
  cs.close();
```

SQL Example

Reset the password of a user named FRED:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_RESET_PASSWORD('fred', 'temppassword');
Statement executed.
```

Reset the password of a user named MrBaseball:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_RESET_PASSWORD('MrBaseball', 'baseball!');
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_MODIFY\_PASSWORD</span>](ModifyPassword.html)

 


