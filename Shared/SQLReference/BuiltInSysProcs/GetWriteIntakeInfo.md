[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetWriteIntakeInfo.html)

<a href="" id="BuiltInSysProcs.GetWriteIntakeInfo"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_WRITE\_INTAKE\_INFO
======================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_WRITE\_INTAKE\_INFO system procedure displays information about the number of writes coming into Splice Machine.

You can use this information to know the number of bulk writes currently active on a server. Each bulk write will contain up to 1000 rows; the compaction and flush queue size, plus the reserved ipc thread setting determine how many writes can execute concurrently.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_WRITE_INTAKE_INFO()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_WRITE\_INTAKE\_INFO</span> include these values:

| Value                    | Description                                                                                                                |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------|
| HOSTNAME                 | The host name.                                                                                                             |
| ACTIVEWRITETHREADS       | The number of active write threads.                                                                                        |
| COMPACTIONQUEUESIZELIMIT | The compaction queue limit at which writes will be blocked.                                                                |
| FLUSHQUEUELIMIT          | The flush queue limit at which writes will be blocked.                                                                     |
| IPCRESERVEDPOOL          | The number of IPC threads reserved for reads.                                                                              
                                                                                                                                                        
                            The maximum number of bulk writes that are allowed currently is equal to the total number of IPC threads minus this value.  |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_WRITE_INTAKE_INFO();
host               |depThreads |indThreads |depCount   |indCount   |avgThroughput         |oneMinAvgThroughput   |fiveMinAvgThroughput  |fifteenMinAvgThroughp&|totalRejected 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
localhost:55709    |0          |0          |0          |0          |0.011451093322589732  |5.472367185912236E-4  |0.007057900046373111  |0.0053884511108858845 |0 

1 row selected
```

 


