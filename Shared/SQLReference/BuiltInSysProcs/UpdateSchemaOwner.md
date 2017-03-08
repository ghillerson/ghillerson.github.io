[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/UpdateSchemaOwner.html)

<a href="" id="BuiltInSysProcs.SetUserAccess"></a>[]()SYSCS\_UTIL.SYSCS\_UPDATE\_SCHEMA\_OWNER
==============================================================================================

The SYSCS\_UTIL.SYSCS\_UPDATE\_SCHEMA\_OWNER system procedure changes the owner of a schema.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_UPDATE_SCHEMA_OWNER(
                         schemaName VARCHAR(128),
                         userName VARCHAR(128))
```

schemaName

Specifies the name of the schema..

userName

Specifies the user ID in the Splice Machine database.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_UPDATE_SCHEMA_OWNER( 'SPLICEBBALL', 'Walt');
Statement executed.
```

 


