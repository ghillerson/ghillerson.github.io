[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysSequences.html)

<a href="" id="SystemTables.SysSequences"></a>[]()SYSSEQUENCES System Table
===========================================================================

The <span class="CodeFont">SYSSEQUENCES</span> table describes the sequence generators in the database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Users should not directly query the <span class="CodeFont">SYSSEQUENCES</span> table, because that will slow down the performance of sequence generators. Instead, users should call the [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE</span> system function](../BuiltInSysProcs/PeekAtSequence.html)

The following table shows the contents of the <span class="CodeFont">SYSSEQUENCES</span> system table.

| Column Name      | Type                                                                        | Length | Nullable | Contents                                                                                                                                                                                                                                  |
|------------------|-----------------------------------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SEQUENCEID       | CHAR                                                                        | 36     | NO       | The ID of the sequence generator. This is the primary key.                                                                                                                                                                                |
| SEQUENCENAME     | VARCHAR                                                                     | 128    | NO       | The name of the sequence generator. There is a unique index on (<span class="CodeFont">SCHEMAID, SEQUENCENAME</span>).                                                                                                                    |
| SCHEMAID         | CHAR                                                                        | 36     | NO       | The ID of the schema that holds the sequence generator. There is a foreign key linking this column to <span class="CodeFont">SYSSCHEMAS.SCHEMAID</span>.                                                                                  |
| SEQUENCEDATATYPE | <span class="ItalicFont">com.splicemachine.db.catalog.TypeDescriptor</span> | -1     | NO       | System type that describes the precision, length, scale, nullability, type name, and storage type of the data                                                                                                                             |
| CURRENTVALUE     | BIGINT                                                                      | 19     | YES      | The current value of the sequence generator. This is not the actual next value for the sequence generator. That value can be obtained by calling the system function <span class="CodeFont">SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE</span>. 
                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                      <span class="CodeFont">SYSSEQUENCES.CURRENTVALUE</span> holds the end of the range of values that have been preallocated in order to boost concurrency. The initial value of this column is <span class="CodeFont">STARTVALUE</span>.      
                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                      This column is <span class="CodeFont">NULL</span> only if the sequence generator is exhausted and cannot issue any more numbers.                                                                                                           |
| STARTVALUE       | BIGINT                                                                      | 19     | NO       | The initial value of the sequence generator                                                                                                                                                                                               |
| MINIMUMVALUE     | BIGINT                                                                      | 19     | NO       | The minimum value of the sequence generator                                                                                                                                                                                               |
| MAXIMUMVALUE     | BIGINT                                                                      | 19     | NO       | The maximum value of the sequence generator                                                                                                                                                                                               |
| INCREMENT        | BIGINT                                                                      | 19     | NO       | The step size of the sequence generator                                                                                                                                                                                                   |
| CYCLEOPTION      | CHAR                                                                        | 1      | NO       | If the sequence generator cycles, this value is <span class="CodeFont">'Y'</span>.                                                                                                                                                        
                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                      If the sequence generator does not cycle, this value is <span class="CodeFont">'N'</span>.                                                                                                                                                 |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


