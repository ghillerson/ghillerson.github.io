[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/Vacuum.html)

<a href="" id="BuiltInSysProcs.Vacuum"></a>[]()SYSCS\_UTIL.VACUUM
=================================================================

The SYSCS\_UTIL.VACUUM system procedure performs the following clean-up operations:

1.  Waits for all previous transactions to complete; at this point, it must be all. If it waits past a certain point, the call terminates, and you will need to run it again.
2.  Gets all the conglomerates that are seen in <span class="CodeFont">sys.sysconglomerates</span> (e.g. <span class="AppCommand">select conglomeratenumber from sys.sysconglomerates</span>).
3.  Gets a list of all of the HBase tables.
4.  If an HBase table is not in the conglomerates list and is not a system table (<span class="CodeFont">conglomeratenumber &lt; 1100 or 1168</span>), then it is deleted.

    If this does not occur, check the <span class="CodeFont">splice.log</span>.

You are ready to go when you see the <span class="AppCommand">Ready to accept connections</span> message.

If you see an exception, but do not see the <span class="AppCommand">Ready to accept connections</span> message, please retry the command.

Syntax

``` FcnSyntax
SYSCS_UTIL.VACUUM()
```

Example

``` Example
splice> CALL SYSCS_UTIL.VACUUM();
Ready to accept connections.
```

 


