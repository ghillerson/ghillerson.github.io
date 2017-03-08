[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowViews.html)

[]()Show Views
==============

The <span class="AppCommand">show views</span> command displays all of the views in the current or specified schema.

Syntax

``` FcnSyntax
SHOW VIEWS [ IN schemaName ] 
```

schemaName

If you supply a schema name, only the views in that schema are displayed; otherwise, the views in the current schema are displayed.

Results

The <span class="AppCommand">show views</span> command results contains the following columns:

| Column Name   | Description                                                               |
|---------------|---------------------------------------------------------------------------|
| TABLE\_SCHEMA | The name of the table's schema                                            |
| TABLE\_NAME   | The name of the table                                                     |
| CONGLOM\_ID   | The conglomerate number, which points to the corresponding table in HBase |
| REMARKS       | Any remarks associated with the table                                     |

Examples

``` AppCommand
splice> show views;
TABLE_SCHEM  |TABLE_NAME         |CONGLOM_ID|REMARKS         
---------------------------------------------------------------
SPLICE       |GUITAR_BRANDS      |4321      |
0 rows selected 
```

 


