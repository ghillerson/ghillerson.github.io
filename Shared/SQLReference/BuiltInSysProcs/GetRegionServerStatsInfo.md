[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetRegionServerStatsInfo.html)

<a href="" id="BuiltInSysProcs.GetRegionServerTaskIno"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_REGION\_SERVER\_STATS\_INFO
==================================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_REGION\_SERVER\_STATS\_INFO system procedure displays input and output statistics about the cluster.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_REGION_SERVER_STATS_INFO()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_REGION\_SERVER\_STATS\_INFO</span> include these values:

| Value             | Description                    |
|-------------------|--------------------------------|
| HOST              | The host name (or IP address). |
| REGIONCOUNT       | The number of regions.         |
| STOREFILECOUNT    | The number of files stored.    |
| WRITEREQUESTCOUNT | The number of write requests.  |
| READREQUESTCOUNT  | The number of read requests.   |
| TOTALREQUESTCOUNT | The total number of requests.  |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_REGION_SERVER_STATS_INFO();
Host          |regionCount         |storeFileCount      |writeRequestCount   |readRequestCount    |totalRequestCount
--------------------------------------------------------------------------------------------------------------------
111.222.3.4   |58                  |0                   |5956                |99697               |20517            
555.666.7.8   |59                  |0                   |1723                |57022               |6253 
1 row selected
```

 


