[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetDatabaseProperty.html)

<a href="" id="BuiltInSysFcns.GetDatabaseProperty"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_DATABASE\_PROPERTY Function
==============================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_DATABASE\_PROPERTY function fetches the value of the specified property of the database on the current connection.

Syntax

``` FcnSyntax
VARCHAR(32672) SYSCS_UTIL.SYSCS_GET_DATABASE_PROPERTY(
  IN Key VARCHAR(128)
  ) 
```

Key

The key for the property whose value you want.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>An error occurs if <span class="ItalicFont">Key</span> is null.

Results

Returns the value of the property. If the value that was set for the property is invalid, the SYSCS\_UTIL.SYSCS\_GET\_DATABASE\_PROPERTY function returns the invalid value, but Splice Machine uses the default value.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

SQL Example

Retrieve the value of the splicemachine.locks.deadlockTimeout property:

``` Example
splice> VALUES SYSCS_UTIL.SYSCS_GET_DATABASE_PROPERTY( 'splicemachine.locks.deadlockTimeout' );
1
-------------------------------------------------------------
10

1 row selected
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY</span>](SetDatabaseProperty.html) built-in system procedure

 


