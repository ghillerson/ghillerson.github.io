[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetSchemaInfo.html)

<a href="" id="BuiltInSysProcs.GetSchemaInfo"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_SCHEMA\_INFO
==========================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_SCHEMA\_INFO system procedure displays table information,including the HBase regions occupied and their store file size, for all user schemas.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_SCHEMA_INFO()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_SCHEMA\_INFO</span> include these values:

| Value        | Description                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| SCHEMANAME   | The schema to which the table belongs.                                                                                                  |
| TABLENAME    | The name of the table. Note that may be more than one row containing a table name; for example, this happens if the table has an index. |
| ISINDEX      | A Boolean value that specifies whether the HBase table is an index table.                                                               |
| HBASEREGIONS | The HBase regions on which the table resides. There can be multiple regions.                                                            
                                                                                                                                                         
                Each region display shows (tableName, regionId.storeFileSize, memStoreSize, and storeIndexSize MB).                                      |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_SCHEMA_INFO();
SCHEMANAME |TABLENAME  |REGIONNAME                                             |IS_I&|HBASEREGIONS_STORES&|MEMSTORESIZE |STOREINDEXSIZE
---------------------------------------------------------------------------------------------------------------------------------------
SPLICE     |PLAYERS    |2176,,1446847689610.7211e284f7f767d7b142dbd639b4d9bf.  |false|0                   |0            |0
SPLICE     |PITCHING   |1968,,1446260714743.01963d7260fc9d4dc01507eccdf67e40.  |false|0                   |0            |0
SPLICE     |BATTING    |1984,,1446260731076.ca29785eb5b16a8752d9c4ceeaad2ce4.  |false|0                   |0            |0
SPLICE     |FIELDING   |2192,,1447092732332.b4aae99023002bbac1a08432e6ffc2df.  |false|0                   |0            |0
SPLICE     |SALARIES   |2256,,1447803176538.11ce38c9e470b4d209de4d32c96cb815.  |false|0                   |0            |0

5 rows selected
```

 


