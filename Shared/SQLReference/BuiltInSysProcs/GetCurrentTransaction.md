[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetCurrentTransaction.html)

<a href="" id="BuiltInSysProcs.DumpTransactions"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_CURRENT\_TRANSACTION
=====================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_CURRENT\_TRANSACTION system procedure displays summary information about the current transaction.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_CURRENT_TRANSACTION()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_CURRENT\_TRANSACTION</span> include these values:

|                                     |                                           |
|-------------------------------------|-------------------------------------------|
| <span class="BoldFont">Value</span> | <span class="BoldFont">Description</span> |
| txnId                               | The ID of the current transaction         |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_CURRENT_TRANSACTION();
txnId
---------------------
2081

1 row selected
```

 


