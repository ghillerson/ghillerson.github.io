[Open topic with navigation](../../index.html#Shared/CmdLineReference/ShowCmds.html)

[]()Show Command
================

The <span class="AppCommand">show</span> command is used to display information about active connections and database objects. You can use a number of different forms of this command to show different types of information, as shown in the following syntax diagram:

Syntax

``` FcnSyntax
SHOW
{
   CONNECTIONS                                 | 
   FUNCTIONS [ IN schemaName ]                 |
   INDEXES [ IN schemaName | FROM table-Name ] |
   PRIMARYKEYS FROM schemaName.FROM tableName  |
   PROCEDURES [ IN schemaName ]                |
   ROLES                                       |
   SCHEMAS                                     |
   SYNONYMS [ IN schemaName ]                  |
   TABLES [ IN schemaName ]                    |
   VIEWS [ IN schemaName ]                     |
}
```

 

Each form of the <span class="CodeFont">SHOW</span> command has its own topic page:

| Command                                     | Description                                                           | Usage                                                                            |
|---------------------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------|
| [show connections](CmdShowConnections.html) | Displays a list of connection names and URLs.                         | <span class="AppCommand">splice&gt; show connections;</span>                     |
| [show functions](CmdShowFunctions.html)     | Displays the functions in a database or in a specific schema.         | <span class="AppCommand">splice&gt; show functions;</span>                       |
| [show indexes](CmdShowIndexes.html)         | Displays the indexes in a database, a schema, or a table.             | <span class="AppCommand">splice&gt; show indexes;</span>                         |
| [show primarykeys](CmdShowPrimaryKeys.html) | Displays the primary keys in a table.                                 | <span class="AppCommand">splice&gt; show primarykeys from myschema.myTbl;</span> |
| [show procedures](CmdShowProcedures.html)   | Displays the procedures that have been created in the database.       | <span class="AppCommand">splice&gt; show procedures;</span>                      |
| [show roles](CmdShowRoles.html)             | Displays a sorted list of all of the roles defined in the database.   | <span class="AppCommand">splice&gt; show roles;</span>                           |
| [show schemas](CmdShowSchemas.html)         | Displays all of the schemas in the current connection.                | <span class="AppCommand">splice&gt; show schemas;</span>                         |
| [show synonyms](CmdShowSynonyms.html)       | Displays the synonyms that have been created in a database or schema. | <span class="AppCommand">splice&gt; show synonyms;</span>                        |
| [show tables](CmdShowTables.html)           | Displays all of the tables in a database or schema.                   | <span class="AppCommand">splice&gt; show tables;</span>                          |
| [show views](CmdShowViews.html)             | Displays all of the views in a schema.                                | <span class="AppCommand">splice&gt; show views;</span>                           |

 


