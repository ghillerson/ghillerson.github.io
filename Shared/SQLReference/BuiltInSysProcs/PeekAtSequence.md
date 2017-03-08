[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/PeekAtSequence.html)

<a href="" id="BuiltInSysFcns.PeekAtSequence"></a>[]()SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE Function
====================================================================================================

The SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE function allows users to observe the instantaneous current value of a sequence generator without having to query the [<span class="CodeFont">SYSSEQUENCES</span> system table](../SystemTables/SysSequences.html).

Querying the <span class="CodeFont">SYSSEQUENCES</span> table does not actually return the current value; it only returns an upper bound on that value, which is the end of the chunk of sequence values that has been pre-allocated but not yet used.

The SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE function shows you the very next value that will be returned by a <span class="CodeFont">NEXT VALUE FOR</span> clause. Users should never directly query the <span class="CodeFont">SYSSEQUENCES</span> table, because that will cause sequence generator concurrency to slow drastically.

Syntax

``` FcnSyntax
BIGINT SYSCS_UTIL.SYSCS_PEEK_AT_SEQUENCE(
            IN SchemaName VARCHAR(128),
            IN SequenceName VARCHAR(128)
            )
```

SchemaName

The name of the schema.

SequenceName

The name of the sequence.

Results

Returns the next value that will be returned for the sequence.

Execute Privileges

By default, all users have execute privileges on this function.

Example

``` Example
splice> VALUES SYSCS_UTIL.SYSCS_PEEK_AT_SEQUENCE('SPLICE', 'PlayerID_seq');
```

See Also

-   [<span class="CodeFont">SYSSEQUENCES</span>](../SystemTables/SysSequences.html) system table

 


