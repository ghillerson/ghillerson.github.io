[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowSynonyms.html)

[]()Show Synonyms
=================

The <span class="AppCommand">show synonyms</span> command displays all of the synonyms that have been created with the <span class="CodeFont">[CREATE SYNONYM](../SQLReference/Statements/CreateSynonym.html)</span> statement in the database or specified schema.

Syntax

``` FcnSyntax
SHOW SYNONYMS [ IN schemaName ] 
```

schemaName

If you supply a schema name, only the synonyms in that schema are displayed; otherwise, all synonyms in the database are displayed.

Results

The <span class="CodeFont">show synonyms</span> command results contains the following columns:

| Column Name   | Description                                                               |
|---------------|---------------------------------------------------------------------------|
| TABLE\_SCHEMA | The name of the synonym's schema                                          |
| TABLE\_NAME   | The name of the table                                                     |
| CONGLOM\_ID   | The conglomerate number, which points to the corresponding table in HBase |
| REMARKS       | Any remarks associated with the table                                     |

Examples

``` AppCommand
splice> show synonyms;
TABLE_SCHEM  |TABLE_NAME         |CONGLOM_ID|REMARKS         
---------------------------------------------------------------
SPLICE       |HITTING            |NULL      |

1 rows selected 
```

 


