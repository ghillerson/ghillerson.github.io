[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetRequests.html)

<a href="" id="BuiltInSysProcs.GetRequests"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_REQUESTS
====================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_REQUESTS system procedure displays information about the number of RPC requests that are coming into Splice Machine.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_REQUESTS()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_REQUESTS</span> include these values:

| Value         | Description                                    |
|---------------|------------------------------------------------|
| HOSTNAME      | The host name.                                 |
| PORT          | The port receiving requests.                   |
| TOTALREQUESTS | The total number of RPC requests on that port. |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_REQUESTS();
HOSTNAME  |PORT  |TOTALREQUE&
-----------------------------------
localhost  |55709 |7296

1 row selected
```

 


