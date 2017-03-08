[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/DropUser.html)

<a href="" id="BuiltInSysProcs.DropUser"></a>[]()SYSCS\_UTIL.SYSCS\_DROP\_USER
==============================================================================

The SYSCS\_UTIL.SYSCS\_DROP\_USER system procedure removes a user account from a database.

This procedure is used in conjunction with NATIVE authentication..

You are not allowed to remove the user account of the database owner.

If you use this procedure to remove a user account, the schemas and data objects owned by the user remain in the database and can be accessed only by the database owner or by other users who have been granted access to them. If the user is created again, then he or she regains access to the schemas and data objects.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_DROP_USER( IN userName VARCHAR(128) )
```

userName

A user name that is case-sensitive if you place the name string in double quotes. This user name is an authorization identifier. If the user name is that of the database owner, an error is raised.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC example

Drop a user named FRED:

``` Example
CallableStatement cs = conn.prepareCall
 ("CALL SYSCS_UTIL.SYSCS_DROP_USER('fred')");
 cs.execute();
 cs.close();
```

SQL Example

Drop a user named FreD:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_DROP_USER('fred');
Statement executed;
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CREATE\_USER</span>](CreateUser.html) built-in system procedure

 


