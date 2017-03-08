[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetActiveServers.html)

<a href="" id="BuiltInSysProcs.GetActiveServers"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_ACTIVE\_SERVERS
================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_ACTIVE\_SERVERS system procedure displays the active servers in the Splice cluster.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_ACTIVE_SERVERS()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_ACTIVE\_SERVERS</span> include these values:

| Value     | Description                                             |
|-----------|---------------------------------------------------------|
| HOSTNAME  | The host on which the server is running.                |
| PORT      | The port on which the server is listening for requests. |
| STARTCODE | The system identifier for the Region Server.            |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_ACTIVE_SERVERS();
HOSTNAME |PORT  |STARTCODE
-------------------------------------
localhost |56412 |1447433590803

1 row selected
```

 


