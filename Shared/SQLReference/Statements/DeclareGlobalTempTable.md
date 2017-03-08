[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DeclareGlobalTempTable.html)

<a href="" id="Statements.CreateGlobalTempTable"></a>[]()DECLARE GLOBAL TEMPORARY TABLE
=======================================================================================

The <span class="CodeFont">DECLARE GLOBAL TEMPORARY TABLE</span> statement defines a temporary table for the current connection.

This statement is similar to the <span class="CodeFont">[CREATE GLOBAL TEMPORARY TABLE](#)</span> and <span class="CodeFont">CREATE LOCAL TEMPORARY TABLE</span> statements, but uses different syntax to provide compatibility with external business intelligence tools.

For general information and notes about using temporary tables, see the [Using Temporary Tables](../../Developers/Fundamentals/TemporaryTables.html) topic in our <span class="ItalicFont">Developer's Guide</span>.

Syntax

``` FcnSyntax
DECLARE GLOBAL TEMPORARY TABLE table-Name
   { column-definition[ , column-definition] * }  
       [ON COMMIT PRESERVE ROWS ]
       [NOT LOGGED]
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine generates a warning if you attempt to specify any other modifiers other than the <span class="CodeFont">NOT LOGGED</span> and <span class="CodeFont">ON COMMIT PRESERVE ROWS</span> modifiers shown above.

table-Name

Names the temporary table.

column-definition

Specifies a column definition. See [column-definition](ColumnDefinition.html) for more information.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You cannot use generated-column-spec in column-definitions for temporary tables.

ON COMMIT PRESERVE ROWS

Specifies that the data in the temporary table is to be preserved until the session terminates.

NOT LOGGED

If you specify this, operations against the temporary table will not be logged; otherwise, logging will take place as usual.

Restrictions on Temporary Tables

You can use temporary tables just like you do permanently defined database tables, with several important exceptions and restrictions that are noted in this section.

Operational Limitations

Temporary tables have the following operational limitations:

-   exist only while a user session is alive
-   are not visible to other sessions or transactions
-   cannot be altered using the <span class="CodeFont">[ALTER TABLE](AlterTable.html)</span>, <span class="CodeFont">[RENAME TABLE](RenameTable.html)</span>, or <span class="CodeFont">[RENAME COLUMN](RenameColumn.html)</span> statements
-   do not get backed up
-   cannot be used as data providers to views
-   cannot be referenced by foreign keys in other tables
-   are not displayed by the <span class="CodeFont">[SHOW](../../CmdLineReference/ShowCmds.html)</span> command

Also note that temporary tables persist across transactions in a session and are automatically dropped when a session terminates.

Table Persistence

Here are two important notes about temporary table persistence. Temporary tables:

-   persist across transactions in a session
-   are automatically dropped when a session terminates or expires

Examples

``` Example
splice> DECLARE GLOBAL TEMPORARY TABLE FirstAndLast(
      id INT NOT NULL PRIMARY KEY, 
      firstName VARCHAR(8) NOT NULL, 
      lastName VARCHAR(10) NOT NULL ) 
   ON COMMIT PRESERVE ROWS
   NOT LOGGED;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">CREATE TEMPORARY TABLE</span>](CreateTempTable.html) statement
-   [Using Temporary Tables](../../Developers/Fundamentals/TemporaryTables.html) in the <span class="ItalicFont">Developer's Guide</span>.

 


