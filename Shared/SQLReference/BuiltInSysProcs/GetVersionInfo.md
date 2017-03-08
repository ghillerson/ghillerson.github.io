[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetVersionInfo.html)

<a href="" id="BuiltInSysProcs.SetUserAccess"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_VERSION\_INFO
===========================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_VERSION\_INFO system procedure sets the connection access permission for the user specified.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_VERSION_INFO()
```

Results

This procedure does not return a result.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_VERSION_INFO();
HOSTNAME       |RELE&|IMPLEMENT&|BUILDTIME             |URL                         
------------------------------------------------------------------------------------
localhost:55709|1.5.1|fe1b10bda0|2015-10-21 13:18 -0500|http://www.splicemachine.com

1 row selected
```

 


