[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/InvalidateStoredStatements.html)

<a href="" id="BuiltInSysProcs.InvalidateStoredStatements"></a>[]()SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS
====================================================================================================================

The SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS system procedure invalidates all system prepared statements, and forces the query optimizer to create new execution plans. You can use this to speed up query execution by the data dictionary when performance has become sub-optimal.

If you notice that <span class="CodeFont">ij show </span>commands have slowed down, you can call <span class="CodeFont">SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS </span>to refresh the execution plans.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> Splice Machine uses prepared statements known as system procedures to access data in the system tables. These procedures are cached, along with their execution plans, in the data dictionary. The cached execution plans can become sub-optimal after you issue a large number of schema-modifying DLL statements, such as defining and/or modifying a number of tables.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_INVALIDATE_STORED_STATEMENTS()
```

Results

This procedure does not return a result.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_INVALIDATE_STORED_STATEMENTS();
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_EMPTY\_GLOBAL\_STATEMENT\_CACHE</span>](EmptyStatementCache.html)
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_EMPTY\_STATEMENT\_CACHE</span>](EmptyStatementCache.html)

 


