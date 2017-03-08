[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/EmptyGlobalStatementCache.html)

<a href="" id="BuiltInSysProcs.EmptyStatementCache"></a>[]()SYSCS\_UTIL.SYSCS\_EMPTY\_GLOBAL\_STATEMENT\_CACHE
==============================================================================================================

The SYSCS\_UTIL.SYSCS\_EMPTY\_GLOBAL\_STATEMENT\_CACHE stored procedure removes as many compiled statements (plans) as possible from the database-wide statement cache (across all region servers).This procedure does not remove statements related to currently executing queries or to activations that are about to be garbage collected, so the cache is not guaranteed to be completely empty after it completes.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The related procedure <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_EMPTY\_STATEMENT\_CACHE](EmptyStatementCache.html)</span> performs the same operation on a single region server.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_EMPTY_GLOBAL_STATEMENT_CACHE()
```

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC Example

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_EMPTY_GLOBAL_STATEMENT_CACHE()");
  cs.execute();
  cs.close();
```

SQL Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_EMPTY_GLOBAL_STATEMENT_CACHE();
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_EMPTY\_STATEMENT\_CACHE</span>](EmptyStatementCache.html)
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS</span>](InvalidateStoredStatements.html)

 


