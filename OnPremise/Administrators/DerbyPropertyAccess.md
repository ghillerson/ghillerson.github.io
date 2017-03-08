[Open topic with navigation](../../index.html#OnPremise/Administrators/DerbyPropertyAccess.html)

[]()Derby Property Access
=========================

This topic describes how to enable and disable Derby features by setting Derby properties, which are divided into categories, as shown in the following table.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When a property value is used, the property is searched for in the order shown in the table; in other words, the property is searched for in the JVM properties; if not found there, it is searched for in the Service properties, then in the Database properties, and finally in the App properties.

| Property Type      | Description                                                                                                                                                                                                                                                                                    |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JVM (System)       | These properties can be as command line arguments to JVM:                                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                                                                                      
                      -   For Maven, include the command line arguments as an <span class="CodeFont">&lt;argument&gt;</span> element in the <span class="CodeFont">pom.xml</span> file. For example:                                                                                                                  
                                                                                                                                                                                                                                                                                                                      
                      ``` AppCommand                                                                                                                                                                                                                                                                                  
                      <argument>-Dderby.language.logStatementText=true</argument>                                                                                                                                                                                                                                     
                      ```                                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                      
                      -   For shell scripts, you may need to manually add the argument to the java executable command line. For example:                                                                                                                                                                              
                                                                                                                                                                                                                                                                                                                      
                      ``` AppCommand                                                                                                                                                                                                                                                                                  
                      java -Dderby.language.logStatementText=true ...                                                                                                                                                                                                                                                 
                      ```                                                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                      
                      System properties can also be set manually using the <span class="CodeFont">System.setProperty(key, value)</span> function.                                                                                                                                                                     |
| Service            | Service properties are a special type of database property that is required to boot the database; as such, these properties cannot be stored in the database. Instead, they are stored outside the database, as follows:                                                                       
                                                                                                                                                                                                                                                                                                                      
                      -   Derby stores service properties in the <span class="CodeFont">service.properties file</span>                                                                                                                                                                                                
                      -   Splice Machine stores service properties in a Zookeeper element.                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                                                      
                      You can temporarily change service properties with the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY](../../Shared/SQLReference/BuiltInSysProcs/SetDatabaseProperty.html)</span> built-in system procedure. These changes will be lost when the server is next restarted.  
                                                                                                                                                                                                                                                                                                                      
                      To make a permanent change in a Derby service property, modify the value in the <span class="CodeFont">service.properties</span> file and then restart the server to apply the changes.                                                                                                         
                                                                                                                                                                                                                                                                                                                      
                      To make a permanent change in a Splice Machine service property, modify the value in ZooKeeper and then restart the server to apply the changes.                                                                                                                                                |
| Database           | Splice Machine database properties are saved in a hidden HBASE table with <span class="CodeFont">CONGLOMERATEID=16</span>.                                                                                                                                                                     |
| App (Derby/Splice) | App properties for both Derby and Splice Machine are saved to the <span class="CodeFont">derby.properties</span> file in the Derby/Splice home directory.                                                                                                                                      
                                                                                                                                                                                                                                                                                                                      
                      App properties can also be saved to these HBASE XML configuration files:                                                                                                                                                                                                                        
                                                                                                                                                                                                                                                                                                                      
                      -   <span class="CodeFont">hbase-default.xml</span>                                                                                                                                                                                                                                             
                      -   <span class="CodeFont">hbase-site.xml</span>                                                                                                                                                                                                                                                
                      -   <span class="CodeFont">splice-site.xml</span>                                                                                                                                                                                                                                               
                                                                                                                                                                                                                                                                                                                      
                      Note that the XML files must reside in the <span class="CodeFont">CLASSPATH</span>.                                                                                                                                                                                                             |

Site File Example
-----------------

The following is an example of a <span class="CodeFont">splice-site.xml</span> file:

``` Example
<?xml version="1.0"?> 
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
   <configuration> 
       <property>
           <name>splice.debug.logStatementContext</name> 
        <value>true</value> 
        <description>Property  to enable logging of all statements.</description> 
    </property> 
    <property> 
        <name>splice.debug.david</name> 
        <value>true</value> 
        <description>Property  to test something.</description> 
    </property> 
   </configuration> 
```

Displaying Derby/Splice Properties
----------------------------------

You can display the Derby/Splice properties with the <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_ALL\_PROPERTIES</span> system procedure, which displays information like this:

``` Example
splice> call SYSCS_UTIL.SYSCS_GET_ALL_PROPERTIES();

KEY                                       |VALUE            |TYPE      
----------------------------------------------------------------------
derby.authentication.builtin.algorithm    |SHA-256          |DATABASE  
derby.user.BROWSE                         |Browse           |APP       
derby.engineType                          |2                |SERVICE   
derby.david.foo                           |WINTERS          |APP       
derby.connection.requireAuthentication    |false            |JVM       
derby.locks.escalationThreshold           |500              |SERVICE   
derby.database.defaultConnectionMode      |fullAccess       |SERVICE   
derby.database.propertiesOnly             |false            |SERVICE   
derby.database.collation                  |UCS_BASIC        |DATABASE  
derby.language.logStatementText           |false            |JVM       
derby.storage.propertiesId                |16               |SERVICE   
derby.language.logQueryPlan               |true             |JVM       
splice.updateSystemProcs                  |false            |JVM       
derby.storage.rowLocking                  |false            |SERVICE   
```

See Also
--------

-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY](../../Shared/SQLReference/BuiltInSysProcs/SetDatabaseProperty.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   The <span class="ItalicFont">Derby Properties Guide</span> on the [Apache Derby documentation site](https://db.apache.org/derby/manuals/index.html).

 


