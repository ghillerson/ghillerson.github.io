[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowTables.html)

[]()Show Tables
===============

The <span class="AppCommand">show tables</span> command displays all of the tables in the current or specified schema.

schemaName

If you supply a schema name, only the tables in that schema are displayed; otherwise, the tables in the current schema are displayed.

Syntax

``` FcnSyntax
SHOW TABLES [ IN schemaName ] 
```

Results

The <span class="CodeFont">show tables</span> command results contains the following columns:

| Column Name   | Description                                                               |
|---------------|---------------------------------------------------------------------------|
| TABLE\_SCHEMA | The name of the table's schema                                            |
| TABLE\_NAME   | The name of the table                                                     |
| CONGLOM\_ID   | The conglomerate number, which points to the corresponding table in HBase |
| REMARKS       | Any remarks associated with the table                                     |

Examples

``` AppCommand
splice> show tables;
TABLE_SCHEM  |TABLE_NAME         |CONGLOM_ID|REMARKS         
-----------------------------------------------------------
SYS          |SYSALIASES         |320       |                
SYS          |SYSCHECKS          |288       |                
SYS          |SYSCOLPERMS        |736       |                
SYS          |SYSCOLUMNS         |48        |                
SYS          |SYSCONGLOMERATES   |64        |                
SYS          |SYSCONSTRAINTS     |352       |                
SYS          |SYSDEPENDS         |336       |                
SYS          |SYSFILES           |384       |                
SYS          |SYSFOREIGNKEYS     |272       |                
SYS          |SYSKEYS            |240       |                
SYS          |SYSPERMS           |832       |                
SYS          |SYSPRIMARYKEYS     |1168      |                
SYS          |SYSROLES           |800       |                
SYS          |SYSROUTINEPERMS    |768       |                
SYS          |SYSSCHEMAS         |32        |                
SYS          |SYSSEQUENCES       |816       |                
SYS          |SYSSTATEMENTS      |256       |                
SYS          |SYSSTATISTICS      |608       |                
SYS          |SYSTABLEPERMS      |672       |                
SYS          |SYSTABLES          |80        |                
SYS          |SYSTRIGGERS        |368       |                
SYS          |SYSUSERS           |896       |                
SYS          |SYSVIEWS           |304       |                
SYSIBM       |SYSDUMMY1          |656       |                
SPLICE       |CUSTOMERS          |1232      |                
SPLICE       |T_DETAIL           |1216      |                
SPLICE       |T_HEADER           |1200      |                

27 rows selected
splice>show tables in SPLICE;

TABLE_SCHEM  |TABLE_NAME         |CONGLOM_ID|REMARKS         
-----------------------------------------------------------
SPLICE       |CUSTOMERS          |1232      |                
SPLICE       |T_DETAIL           |1216      |                
SPLICE       |T_HEADER           |1200      |                

3 rows selected
```

 


