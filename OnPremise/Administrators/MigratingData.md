[Open topic with navigation](../../index.html#OnPremise/Administrators/MigratingData.html)

Migrating Your Splice Machine Database
======================================

This topic describes how to migrate your Splice Machine database to the latest version of Splice Machine software using the <span class="ItalicFont">Splice Machine Migration Assistant</span>.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: This feature is available only with a Splice Machine Enterprise license.</span>

You cannot use this feature with the Community version of Splice Machine. For a list of the additional features available in the Enterprise edition, see our [Splice Machine Editions](../GettingStarted/SpliceEditions.html) page.

To obtain a license for the Splice Machine <span class="ItalicFont">Enterprise Edition</span>, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

You can complete the migration process in these simple steps:

1.  <a href="#Download" class="MCXref xref">Download and Install the Migration Assistant</a>
2.  <a href="#Use" class="MCXref xref">Use the Migration Assistant to Export Your Database</a>
3.  <a href="#Update" class="MCXref xref">Update to the Latest Version of Splice Machine</a>
4.  <a href="#Use2" class="MCXref xref">Use the Migration Assistant to Import Your Database</a>

You use the same Migration Assistant tool to export your database before updating your Splice Machine installation, and to subsequently import your database after updating.

[]()Download and Install the Migration Assistant
------------------------------------------------

To download and install the <span class="ItalicFont">Splice Machine Migration Assistant</span> tool, follow these steps:

1.  Verify prerequisites:

    Make sure that you have version 1.8 (or later) of the JRE installed on the node. You can view the version of JRE installed on most computers by using the following command:

    ``` ShellCommand
    java -XshowSettings:properties -version
    ```

2.  Download the Migration Assistant:

    Download the tool in compressed archive format to the home directory of your standalone computer or to any node in your cluster. You'll find <span class="CodeFont">gz</span> and <span class="CodeFont">zip</span> versions of the the download package here:

    ``` Plain
    https://console.aws.amazon.com/s3/home?region=us-west-2#&bucket=cetera-poc&prefix=ddlutils/Migration%20Assistant/
    ```

3.  Unpackage the Tool:

    Unpackage the archive you downloaded on your node, which contains these files:

    | File                         | Description                                                                                                                       |
    |------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
    | Migration.sh                 | The script you use to run the Migration Assistant once you have the configuration file set up.                                    |
    | ddlutils-&lt;version&gt;.jar | The Migration Assistant code.                                                                                                     |
    | README.md                    | The Read Me file for the Migration Assistant.                                                                                     |
    | prop.cfg                     | The configuration file used by the Migration Assistant. You need to modify this file before exporting or importing your database. |

[]()Use the Migration Assistant to Export Your Database
-------------------------------------------------------

To export your database prior to upgrading your Splice Machine software, you need to:

1.  Edit the <span class="CodeFont">prop.cfg</span> file with your desired configuration settings. See the <a href="#Migratio" class="MCXref xref">Migration Assistant Configuration Settings</a> section below for details. Make sure that you have the <span class="CodeFont">operation</span> property set to <span class="CodeFont">backup</span>.
2.  Verify that permissions are set correctly for the directory you specify for bad record information is in HDFS (the value of the <span class="CodeFont">hdfsBadDir</span> configuration setting); substitute that directory name for <span class="HighlightedCode">&lt;hdfsBadDir&gt;</span> in the following command line:

    ``` ShellCommand
    chmod 777 <hdfsBadDir>
    ```

3.  Verify that the directory you specify for the work file (the value of the <span class="CodeFont">hdfsWorkDir</span> configuration property) is present on the computer you're using.
4.  Run the <span class="CodeFont">Migration.sh</span> script to export your database.
5.  Examine the log file to verify that the export worked as you expect.

    See <a href="#The" class="MCXref xref">The Export Log File</a> section below for details on the generated log table.

[]()Update to the Latest Version of Splice Machine
--------------------------------------------------

Follow the update instructions in our [Installation Guide](../InstallingSpliceMachine/Intro.InstallationGuide.html) to update to the latest version of Splice Machine.

[]()Use the Migration Assistant to Import Your Database
-------------------------------------------------------

After you've upgraded your database, you can use the Migration Assistant a second time to restore the database you previously exported. Follow these steps:

1.  Verify that the Splice Machine region servers are running after the upgrade. You can easily verify this by issuing the following commands at the splice&gt; command prompt:

    ``` Example
    splice> select * from SYS.SYSTABLES;
    splice> select * from SYS.SYSTABLES --splice-properties useSpark=true
    > ;
    ```

2.  Edit the <span class="CodeFont">prop.cfg</span> file with your desired configuration settings. Make sure that you change the the <span class="CodeFont">operation</span> property set to <span class="CodeFont">restore</span>.
3.  Update any settings that start with import, as required. See the <a href="#Migratio" class="MCXref xref">Migration Assistant Configuration Settings</a> section below for details.
4.  Run the <span class="CodeFont">Migration.sh</span> script to import your upgraded database.
5.  Examine the log file to verify that the export worked as you expect. See <a href="#The" class="MCXref xref">The Export Log File</a> section below for details on the generated log table.
6.  You should also verify that your database has been restored.

[]()Migration Assistant Configuration Settings
----------------------------------------------

The following table describes the configuration properties you can specify in the Migration Assistant's <span class="CodeFont">prop.cfg</span> file.

| Property Name         | Description                                                                                                                                                                                                                                          |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| operation             | The Migration Assistant offers two operation modes:                                                                                                                                                                                                  
                                                                                                                                                                                                                                                                               
                         |         |                                                                                    |                                                                                                                                                      
                         |---------|------------------------------------------------------------------------------------|                                                                                                                                                      
                         | backup  | Prepare your database for upgrade by exporting it.                                 |                                                                                                                                                      
                         | restore | Restore your database after upgrading by importing a previously exported database. |                                                                                                                                                      |
| fileWorkDir           | The path of the directory in the local file system of the node on which you are running the Migration Assistant the local file system                                                                                                                |
| hdfsDataDir           | The path to the working directory in HDFS in which the exported/imported data files are stored. Each table's data is stored in a separate file that is named as (with bracketed values replaced by your actual directory, schema, and table names)d: 
                                                                                                                                                                                                                                                                               
                         ``` Plain                                                                                                                                                                                                                                             
                         <hdfsDataDir>/<schema-name>/<table-name>/<backedup data>.csv                                                                                                                                                                                          
                         ```                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                               
                         Note that you can verify data that has been written with commands such as the following:                                                                                                                                                              
                                                                                                                                                                                                                                                                               
                         ``` ShellCommand                                                                                                                                                                                                                                      
                         sudo su <userId>                                                                                                                                                                                                                                      
                         hadoop fs -ls /<hdfsDataDir>/<schema-name>/<table-name>/*                                                                                                                                                                                             
                         ```                                                                                                                                                                                                                                                   |
| hdfsBadDir            | The path to the directory in which you want all bad record information recorded.                                                                                                                                                                     
                                                                                                                                                                                                                                                                               
                         If you do not specify a directory here, then all errors found in a specific table are stored in a subdirectory of the <span class="CodeFont">hdfsDataDir</span> directory:                                                                            
                                                                                                                                                                                                                                                                               
                         ``` Plain                                                                                                                                                                                                                                             
                         <hdfsDataDir>/<schema-name>/<table-name>/                                                                                                                                                                                                             
                         ```                                                                                                                                                                                                                                                   |
| tables                | Specifies which tables and schemas you want to upgrade (export and then import). Leave this blank if you want all schemas and tables in your data upgraded.                                                                                          
                                                                                                                                                                                                                                                                               
                         If you want to upgrade only a specific schema or set of schemas, use a list; for example:                                                                                                                                                             
                                                                                                                                                                                                                                                                               
                         ``` Example                                                                                                                                                                                                                                           
                         SPLICE.*,MYSCHEMA.*                                                                                                                                                                                                                                   
                         ```                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                               
                         If you want to upgrade only a specific table or set of tables, use a list; for example:                                                                                                                                                               
                                                                                                                                                                                                                                                                               
                         ``` Example                                                                                                                                                                                                                                           
                         SPLICE.MyTable1,SPLICE.MyTable2                                                                                                                                                                                                                       
                         ```                                                                                                                                                                                                                                                   |
| multilineImportTables | A Boolean value that specifies whether each line in the import file contains one complete record. Use one of the following values:                                                                                                                   
                                                                                                                                                                                                                                                                               
                         |      |                                                  |                                                                                                                                                                                           
                         |------|--------------------------------------------------|                                                                                                                                                                                           
                         | null | Each record is stored in one line in the file.   |                                                                                                                                                                                           
                         | true | Each record can span multiple lines in the file. |                                                                                                                                                                                           |
| exportObject          | Which object types to export from your database; specify one of the following values:                                                                                                                                                                
                                                                                                                                                                                                                                                                               
                         |      |                                                       |                                                                                                                                                                                      
                         |------|-------------------------------------------------------|                                                                                                                                                                                      
                         | ddl  | Import only the data definitions, not the data.       |                                                                                                                                                                                      
                         | data | Import only the data, not the data definitions.       |                                                                                                                                                                                      
                         | all  | Import all of the exported data definitions and data. |                                                                                                                                                                                      |
| exportServers         | The name of the server(s) to use for exporting the data. You can use a comma-separated list to specify multiple servers; for example:                                                                                                                
                                                                                                                                                                                                                                                                               
                         ``` Example                                                                                                                                                                                                                                           
                         server-011, server-02, server-03                                                                                                                                                                                                                      
                         ```                                                                                                                                                                                                                                                   |
| exportDbUser          | The user ID to use for the upgraded database when you export it.                                                                                                                                                                                     
                                                                                                                                                                                                                                                                               
                         The default user ID for Splice Machine databases is <span class="CodeFont">splice</span>.                                                                                                                                                             |
| exportDbPassword      | The password to use for the upgraded database when you export it.                                                                                                                                                                                    
                                                                                                                                                                                                                                                                               
                         The default password for Splice Machine databases is <span class="CodeFont">admin</span>.                                                                                                                                                             |
| exportThreadCount     | The number of export threads to use. You can increase the default value (1 thread) to improve performance.                                                                                                                                           |
| importObject          | Which object types to import from the previously exported file; specify one of the following values:                                                                                                                                                 
                                                                                                                                                                                                                                                                               
                         |      |                                                       |                                                                                                                                                                                      
                         |------|-------------------------------------------------------|                                                                                                                                                                                      
                         | ddl  | Import only the data definitions, not the data.       |                                                                                                                                                                                      
                         | data | Import only the data, not the data definitions.       |                                                                                                                                                                                      
                         | all  | Import all of the exported data definitions and data. |                                                                                                                                                                                      |
| importServers         | The name of the server(s) to use for importing the data. You can use a comma-separated list to specify multiple servers; for example:                                                                                                                
                                                                                                                                                                                                                                                                               
                         ``` Example                                                                                                                                                                                                                                           
                         server-011, server-02, server-03                                                                                                                                                                                                                      
                         ```                                                                                                                                                                                                                                                   |
| importDbUser          | The user ID to use for the upgraded database when you import it. This is typically the same user ID specified in the <span class="CodeFont">importDbPassword</span> property.                                                                        
                                                                                                                                                                                                                                                                               
                         The default user ID for Splice Machine databases is <span class="CodeFont">splice</span>.                                                                                                                                                             |
| importDbPassword      | The password to use for the upgraded database when you import it. This is typically the same password specified in the <span class="CodeFont">exportDbPassword</span> property.                                                                      
                                                                                                                                                                                                                                                                               
                         The default password for Splice Machine databases is <span class="CodeFont">admin</span>.                                                                                                                                                             |
| importThreadCount     | The number of import threads to use. You can increase the default value (1 thread) to improve performance.                                                                                                                                           |

[]()The Export Log File
-----------------------

The following table shows the contents of the <span class="CodeFont">EXPORT\_IMPORT\_LOG</span> file that the Migration Assistant generates..

| Column Name        | Type         | Description                                                         |
|--------------------|--------------|---------------------------------------------------------------------|
| S\_NO              | INTEGER      | GENERATED BY DEFAULT AS IDENTITY                                    
                                     (start with 0, increment by 1)                                       |
| SCHEMA\_NAME       | VARCHAR(100) | The name of the schema being processed.                             |
| TABLE\_NAME        | VARCHAR(100) | The name of the table being processed.                              |
| DDL\_EXPORT\_FLAG  | CHAR(1)      | The status of the DDL export; this is one of the following values:  
                                                                                                          
                                     |      |                                  |                          
                                     |------|----------------------------------|                          
                                     | S    | The operation was successful.    |                          
                                     | F    | The operation failed.            |                          
                                     | null | The operation was not performed. |                          |
| DDL\_EXPORT\_TS    | TIMESTAMP    | The time at which the DDL export was performed.                     |
| DATA\_EXPORT\_FLAG | CHAR(1)      | The status of the data export; this is one of the following values: 
                                                                                                          
                                     |      |                                  |                          
                                     |------|----------------------------------|                          
                                     | S    | The operation was successful.    |                          
                                     | F    | The operation failed.            |                          
                                     | null | The operation was not performed. |                          |
| DATA\_EXPORT\_TS   | TIMESTAMP    | The time at which the data export was performed.                    |
| DDL\_IMPORT\_FLAG  | CHAR(1)      | The status of the DDL import; this is one of the following values:  
                                                                                                          
                                     |      |                                  |                          
                                     |------|----------------------------------|                          
                                     | S    | The operation was successful.    |                          
                                     | F    | The operation failed.            |                          
                                     | null | The operation was not performed. |                          |
| DDL\_IMPORT\_TS    | TIMESTAMP    | The time at which the DDL import was performed.                     |
| DATA\_IMPORT\_FLAG | CHAR(1)      | The status of the data import; this is one of the following values: 
                                                                                                          
                                     |      |                                  |                          
                                     |------|----------------------------------|                          
                                     | S    | The operation was successful.    |                          
                                     | F    | The operation failed.            |                          
                                     | null | The operation was not performed. |                          |
| DATA\_IMPORT\_TS   | TIMESTAMP    | The time at which the data import was performed.                    |

 

 


