[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Intro.Statements.html)

[]()Statements
==============

This section contains the reference documentation for the Splice Machine SQL Statements, in the following subsections:

-   [Data Definition (DDL) - General Statements](Intro.DDLStatements.html)
-   [Data Definition (DDL) - Create Statements](Intro.DDLCreateStatements.html)
-   [Data Definition (DDL) - Drop Statements](Intro.DDLDropStatements.html)
-   [Data Manipulation (DML) Statements](Intro.DMLStatements.html)
-   [Session Control Statements](#Session)

Data Definition - General Statements

These are the [data definition statements](Intro.DDLStatements.html):

| Statement                            | Description                                                                                |
|--------------------------------------|--------------------------------------------------------------------------------------------|
| [ALTER TABLE](AlterTable.html)       | Add, deletes, or modifies columns in an existing table.                                    |
| [GRANT](Grant.html)                  | Gives privileges to specific user(s) or role(s) to perform actions on database objects.    |
| [PIN TABLE](PinTable.html)           | Caches a table in memory for improved performance.                                         |
| [RENAME COLUMN](RenameColumn.html)   | Renames a column in a table.                                                               |
| [RENAME INDEX](RenameIndex.html)     | Renames an index in the current schema.                                                    |
| [RENAME TABLE](RenameTable.html)     | Renames an existing table in a schema.                                                     |
| [REVOKE](Revoke.html)                | Revokes privileges for specific user(s) or role(s) to perform actions on database objects. |
| [TRUNCATE TABLE](TruncateTable.html) | Resets a table to its initial empty state.                                                 |
| [UNPIN TABLE](UnpinTable.html)       | Unpins a pinned (cached) table.                                                            |

Data Definition (DDL) - CREATE Statements

These are the [create statements](Intro.DDLCreateStatements.html):

| Statement                                                     | Description                                                                                                                                     |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| [CREATE EXTERNAL TABLE](CreateExternalTable.html)             | Allows you to query data stored in a flat file as if that data were stored in a Splice Machine table.                                           |
| [CREATE FUNCTION](CreateFunction.html)                        | Creates Java functions that you can then use in expressions.                                                                                    |
| [CREATE INDEX](CreateIndex.html)                              | Creates an index on a table.                                                                                                                    |
| [CREATE PROCEDURE](CreateProcedure.html)                      | Creates Java stored procedures, which you can then call using the [<span class="CodeFont">Call Procedure</span>](CallProcedure.html) statement. |
| [CREATE ROLE](CreateRole.html)                                | Creates SQL roles.                                                                                                                              |
| [CREATE SCHEMA](CreateSchema.html)                            | Creates a schema.                                                                                                                               |
| [CREATE SEQUENCE](CreateSequence.html)                        | Creates a sequence generator, which is a mechanism for generating exact numeric values, one at a time.                                          |
| [CREATE SYNONYM](CreateSynonym.html)                          | Creates a synonym, which can provide an alternate name for a table or a view.                                                                   |
| [CREATE TABLE](CreateTable.html)                              | Creates a new table.                                                                                                                            |
| [CREATE TEMPORARY TABLE](CreateTempTable.html)                | Defines a temporary table for the current connection.                                                                                           |
| [CREATE TRIGGER](CreateTrigger.html)                          | Creates a trigger, which defines a set of actions that are executed when a database event occurs on a specified table                           |
| [CREATE VIEW](CreateView.html)                                | Creates a view, which is a virtual table formed by a query.                                                                                     |
| [DECLARE GLOBAL TEMPORARY TABLE](DeclareGlobalTempTable.html) | Defines a temporary table for the current connection.                                                                                           |

Data Definition (DDL) - DROP Statements

These are the [drop statements](Intro.DDLDropStatements.html):

| Statement                            | Description                        |
|--------------------------------------|------------------------------------|
| [DROP FUNCTION](DropFunction.html)   | Drops a function from a database.  |
| [DROP INDEX](DropIndex.html)         | Drops an index from a database.    |
| [DROP PROCEDURE](DropProcedure.html) | Drops a procedure from a database. |
| [DROP ROLE](DropRole.html)           | Drops a role from a database.      |
| [DROP SCHEMA](DropSchema.html)       | Drops a schema from a database.    |
| [DROP SEQUENCE](DropSequence.html)   | Drops a sequence from a database.  |
| [DROP SYNONYM](DropSynonym.html)     | Drops a synonym from a database.   |
| [DROP TABLE](DropTable.html)         | Drops a table from a database.     |
| [DROP TRIGGER](DropTrigger.html)     | Drops a trigger from a database.   |
| [DROP VIEW](DropView.html)           | Drops a view from a database.      |
| [DROP FUNCTION](DropFunction.html)   | Drops a function from a database.  |

Data Manipulation (DML) Statements

These are the [data manipulation statements](Intro.DMLStatements.html):

| Statement                            | Description                   |
|--------------------------------------|-------------------------------|
| [CALL PROCEDURE](CallProcedure.html) | Calls a stored procedure.     |
| [DELETE](Delete.html)                | Deletes records from a table. |
| [INSERT](Insert.html)                | Inserts records into a table. |
| [SELECT](Select.html)                | Selects records.              |
| [UPDATE TABLE](UpdateTable.html)     | Updates values in a table.    |

[]()Session Control Statements

These are the [session control statements](Intro.SessionControlStatements.html):

| Statement                    | Description                                                     |
|------------------------------|-----------------------------------------------------------------|
| [SET ROLE](SetRole.html)     | Sets the current role for the current SQL context of a session. |
| [SET SCHEMA](SetSchema.html) | Sets the default schema for a connection's session.             |

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

 


