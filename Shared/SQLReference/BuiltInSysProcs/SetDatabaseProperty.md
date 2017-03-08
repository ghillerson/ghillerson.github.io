[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/SetDatabaseProperty.html)

<a href="" id="BuiltInSysProcs.SetDatabaseProperty"></a>[]()SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY
======================================================================================================

Use the SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY system procedure to set or delete the value of a property of the database on the current connection.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY(
          IN key VARCHAR(128),
          IN value VARCHAR(32672)
)
```

key

The property name.

value

The new property value. If this is <span class="CodeFont">null</span>, then the property with key value <span class="CodeFont">key</span> is deleted from the database property set. If this is not <span class="CodeFont">null</span>, then this <span class="CodeFont">value</span> becomes the new value of the property. If this value is not a valid value for the property, Splice Machine uses the default value of the property.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC example

Set the splicemachine.locks.deadlockTimeout property to a value of 10:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY(?, ?)");
  cs.setString(1, "splicemachine.locks.deadlockTimeout");
  cs.setString(2, "10");
  cs.execute();
  cs.close();
```

SQL Example

Set the splicemachine.locks.deadlockTimeout property to a value of 10:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY( 'splicemachine.locks.deadlockTimeout', '10' );
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_DATABASE\_PROPERTY</span>](GetDatabaseProperty.html) built-in system function

 


