[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/CreateUser.html)

<a href="" id="BuiltInSysProcs.CreateUser"></a>[]()SYSCS\_UTIL.SYSCS\_CREATE\_USER
==================================================================================

The SYSCS\_UTIL.SYSCS\_CREATE\_USER system procedure adds a new user account to a database.

This procedure creates users for use with NATIVE authentication.

If NATIVE authentication is not already turned on when you call this procedure:

-   The first user whose credentials are stored must be the database owner.
-   Calling this procedure will turn on NATIVE authentication the next time the database is booted.

Once you turn on NATIVE authentication with this procedure, it remains turned on permanently. There is no way to turn it off.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_CREATE_USER(
        IN userName VARCHAR(128),
        IN password VARCHAR(32672)
        )
```

userName

A user name that is case-sensitive if you place the name string in double quotes. This user name is an authorization identifier.

Case sensitivity is very specific with user names: if you specify the user name in single quotes, e.g. 'Fred', the system automatically converts it into all Uppercase.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The user name is only case sensitive if you double-quote it inside of the single quotes. For example, <span class="CodeFont">'"Fred"'</span> is a different user name than <span class="CodeFont">'Fred'</span>, because <span class="CodeFont">'Fred'</span> is assumed to be case-insensitive.

password

A case-sensitive password.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC example

Create a user named FRED:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_CREATE_USER(?, ?)");
  cs.setString(1, "fred");
  cs.setString(2, "fredpassword");
  cs.execute();
  cs.close();
```

Create a user named FreD:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_CREATE_USER(?, ?)");
  cs.setString(1, "\"FreD\"");
  cs.setString(2, "fredpassword");
  cs.execute();
  cs.close();
```

SQL Example

Create a user named FRED:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_CREATE_USER('fred', 'fredpassword');
Statement executed.
```

Create a (case sensitive) user named <span class="CodeFont">MrBaseball</span>:

``` Example
CALL SYSCS_UTIL.SYSCS_CREATE_USER('MrBaseball', 'pinchhitter')
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DROP\_USER</span>](DropUser.html) built-in system procedure

 


