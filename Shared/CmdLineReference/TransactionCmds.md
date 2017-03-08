[Open topic with navigation](../../index.html#Shared/CmdLineReference/TransactionCmds.html)

[]()Transaction Commands
========================

This section describes the <span class="AppCommand">splice&gt;</span> commands you use to work with transactions in your database:

| Command                                              | Description                                                                  | Usage                                                                                 |
|------------------------------------------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| [Autocommit](CmdAutocommit.html)                     | Turns the connection's auto-commit mode on or off.                           | <span class="AppCommand">splice&gt; autocommit off;</span>                            |
| [Commit](CmdCommit.html)                             | Commits the currently active transaction and initiates a new transaction.    | <span class="AppCommand">splice&gt; commit;</span>                                    |
| [Connect](CmdConnect.html)                           | Connect to a database via its URL.                                           | <span class="AppCommand">splice&gt; connect 'jdbc:splice://xyz:1527/splicedb';</span> |
| [Release Savepoint](CmdReleaseSavepoint.html)        | Releases a savepoint.                                                        | <span class="AppCommand">splice&gt; release savepoint gSavePt1;</span>                |
| [Rollback](CmdRollback.html)                         | Rolls back the currently active transaction and initiates a new transaction. | <span class="AppCommand">splice&gt; rollback;</span>                                  |
| [Rollback to Savepoint](CmdRollbackToSavepoint.html) | Rolls the current transaction back to the specified savepoint.               | <span class="AppCommand">splice&gt; rollback to savepoint gSavePt1;</span>            |
| [Savepoint](CmdSavepoint.html)                       | Creates a savepoint within the current transaction.                          | <span class="AppCommand">splice&gt; savepoint gSavePt1;</span>                        |

 


