[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetAllProperties.html)

<a href="" id="BuiltInSysProcs.GetActiveServers"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_ALL\_PROPERTIES
================================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_ALL\_PROPERTIES system procedure displays all of the Splice Machine Derby properties.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_ALL_PROPERTIES()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_ALL\_PROPERTIES</span> include these values:

| Value | Description        |
|-------|--------------------|
| KEY   | The property name  |
| VALUE | The property value |
| TYPE  | The property type  |

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_ALL_PROPERTIES();
KEY                                               |VALUE                                   |TYPE      
------------------------------------------------------------------------------------------------------
derby.authentication.builtin.algorithm            |SHA-512                                 |JVM       
derby.authentication.native.create.credentials.da&|true                                    |JVM       
derby.authentication.provider                     |NATIVE:spliceDB:LOCAL                   |JVM       
derby.connection.requireAuthentication            |true                                    |JVM       
derby.database.collation                          |UCS_BASIC                               |DATABASE  
derby.database.defaultConnectionMode              |fullAccess                              |SERVICE   
derby.database.propertiesOnly                     |false                                   |SERVICE   
derby.database.sqlAuthorization                   |true                                    |JVM       
derby.engineType                                  |2                                       |SERVICE   
derby.language.logQueryPlan                       |false                                   |SERVICE   
derby.language.logStatementText                   |false                                   |SERVICE   
derby.language.updateSystemProcs                  |false                                   |JVM       
derby.locks.escalationThreshold                   |500                                     |SERVICE   
derby.storage.propertiesId                        |16                                      |SERVICE   
derby.storage.rowLocking                          |false                                   |SERVICE   
derby.stream.error.file                           |./splice-derby.log                      |JVM       
splice.authentication                             |NATIVE                                  |JVM       
splice.debug.logStatementContext                  |false                                   |JVM       
splice.software.buildtime                         |2015-10-21 13:18 -0500                  |JVM       
splice.software.release                           |1.5.1                                   |JVM       
splice.software.url                               |http://www.splicemachine.com            |JVM       
splice.software.versionhash                       |fe1b10bda0                              |JVM       

22 rows selected
```

 


