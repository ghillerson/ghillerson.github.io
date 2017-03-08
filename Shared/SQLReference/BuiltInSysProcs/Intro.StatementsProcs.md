[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/Intro.StatementsProcs.html)

[]()Statement and Stored Procedure System Procedures and Functions
==================================================================

These are the system procedures and functions for working with executing statements and stored procedures:

| Procedure / Function Name                                                            | Description                                                                                                                 |
|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_EMPTY\_GLOBAL\_STATEMENT\_CACHE](EmptyGlobalStatementCache.html) | Removes as many compiled statements (plans) as possible from the database-wide statement cache (across all region servers). |
| [SYSCS\_UTIL.SYSCS\_EMPTY\_STATEMENT\_CACHE](EmptyStatementCache.html)               | Removes as many compiled statements (plans) as possible from the database statement cache on your current region server.    |
| [SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS](InvalidateStoredStatements.html) | Invalidates all system prepared statements and forces the query optimizer to create new execution plans.                    |
| [SYSCS\_UTIL.SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES](UpdateAllSystemProcedures.html) | Updates the signatures of all of the system procedures in a database.                                                       |
| [SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE](UpdateSystemProcedure.html)           | Updates the stored declaration of a specific system procedure in the data dictionary.                                       |

 


