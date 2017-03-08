[Open topic with navigation](../../index.html#OnPremise/GettingStarted/SpliceCmdLine.html)

[]()The splice&gt; Command Line Interface
=========================================

This topic introduces the Splice Machine command line interface, which is also referred to as the <span class="AppCommand">splice&gt;</span> prompt; it contains a [summary of the available commands](#Commands).

The <span class="ItalicFont">Splice Machine Command Line Reference</span> is a complete reference manual for the <span class="AppCommand">splice&gt;</span> command line interpreter; it:

-   specifies the [syntax rules](../../Shared/CmdLineReference/CmdLineSyntax.html) of the command line interpreter
-   tells you how you can script <span class="AppCommand">splice&gt;</span> commands to run a series of operations like loading a number of files into your database.
-   contains a [Commands Reference](../../Shared/CmdLineReference/CmdLineSummary.html) section with a reference page for each of the <span class="AppCommand">splice&gt;</span> commands.

[]()Starting the <span class="AppCommand">splice&gt;</span> Command Line Interface
----------------------------------------------------------------------------------

You start the <span class="AppCommand">splice&gt;</span> prompt by running the <span class="CodeFont">sqlshell.sh</span> script, the location of which depends on your platform:

| Hadoop platform                                                            | Location of sqlshell.sh                                                                         | Notes                                                                                                                                                                                                                                                                           |
|----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span class="PlatformVariablesCDH5Versions">CDH 5.7.2, 5.8.0, 5.8.3</span> | <span class="PlatformVariablesCDHStartCmdLine">/opt/cloudera/parcels/CDH/bin/sqlshell.sh</span> | You may need to create symbolic links to the JDK that was installed by Cloudera Manager so that the JDK is in the system path on each node, if it's not already there. Use commands like these:                                                                                 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
                                                                                                                                                                                ``` ShellCommand                                                                                                                                                                                                                                                                 
                                                                                                                                                                                sudo ln -s /usr/java/jdk1.7.0_67-cloudera /usr/java/default                                                                                                                                                                                                                      
                                                                                                                                                                                sudo ln -s /usr/java/default/bin/java /usr/bin/java                                                                                                                                                                                                                              
                                                                                                                                                                                ```                                                                                                                                                                                                                                                                              |
| <span class="PlatformVariablesHDP2Versions">HDP 2.4.2 and 2.5</span>       | <span class="PlatformVariablesHDP2StartCmdLine">~/sqlshell.sh</span>                            | The <span class="CodeFont">sqlshell.sh</span> script is found in the home directory of the cluster administrator user on each RegionServer node.                                                                                                                                |
| <span class="PlatformVariablesMapR5Versions">MapR 5.1.0 and 5.2.0</span>   | <span class="PlatformVariablesMapRStartCmdLine">~/sqlshell.sh</span>                            | The <span class="CodeFont">sqlshell.sh</span> script is found in the home directory of the cluster administrator user on each RegionServer node.                                                                                                                                |
| Standalone version                                                         | <span class="PlatformVariablesStandaloneStartCmdLine">splicemachine/bin/sqlshell.sh</span>      | If you are running the standalone version of Splice Machine on a computer that goes into sleep mode, you will need to exit the command line, [stop your database](../Administrators/ShuttingDownDatabase.html), and [then restart it](../Administrators/StartingDatabase.html). |

Running a file of SQL commands with the <span class="AppCommand">splice&gt;</span> Command Line Interface
---------------------------------------------------------------------------------------------------------

You can invoke <span class="AppCommand">sqlshell.sh</span> with the <span class="AppCommand">-f</span> argument to start the command line interpreter, run a set of <span class="AppCommand">splice&gt;</span> commands stored in a file, and then exit. The following is an example of using this option:

``` ShellCommand
$ ./sqlshell.sh -f /home/mydir/sql/test.sql

 ========= rlwrap detected and enabled.  Use up and down arrow keys to scroll through command line history. ======== 

Running Splice Machine SQL shell
For help: "splice> help;"
SPLICE* - jdbc:splice://10.1.1.111:1527/splicedb
* = current connection
splice> elapsedtime on;
splice> select count(*) from CUST_EMAIL;
1                   
--------------------
0                   

1 row selected
ELAPSED TIME = 6399 milliseconds
splice> 
$ 
```

The <span class="CodeFont">test.sql</span> file used in the above example contains the following

``` ShellCommand
elapsedtime on;
select count(*) from CUST_EMAIL;
```

[]()Commands Summary
--------------------

The following table summarizes the commands you can enter in response to the <span class="AppCommand">splice&gt;</span> prompt. You can find a reference page for each command in the Commands Reference Click a command name in the table to view the command's reference page.

| Command                                                                            | Description                                                                                            | Usage                                                                                                                                           |
|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| [Analyze](../../Shared/CmdLineReference/CmdAnalyze.html)                           | Collects statistics for a table or schema                                                              | <span class="AppCommand">splice&gt; analyze table myTable;                                                                                      
                                                                                                                                                                                               splice&gt; analyze schema myschema;</span>                                                                                                       |
| [Autocommit](../../Shared/CmdLineReference/CmdAutocommit.html)                     | Turns the connection's auto-commit mode on or off.                                                     | <span class="AppCommand">splice&gt; autocommit off;</span>                                                                                      |
| [Commit](../../Shared/CmdLineReference/CmdCommit.html)                             | Commits the currently active transaction and initiates a new transaction.                              | <span class="AppCommand">splice&gt; commit;</span>                                                                                              |
| [Connect](../../Shared/CmdLineReference/CmdConnect.html)                           | Connect to a database via its URL.                                                                     | <span class="AppCommand">splice&gt; connect 'jdbc:splice://xyz:1527/splicedb';</span>                                                           |
| [Describe](../../Shared/CmdLineReference/CmdDescribe.html)                         | Displays a description of a table or view.                                                             | <span class="AppCommand">splice&gt; describe myTable;</span>                                                                                    |
| [Disconnect](../../Shared/CmdLineReference/CmdDisconnect.html)                     | Disconnects from a database.                                                                           | <span class="AppCommand">splice&gt; disconnect SPLICE;</span>                                                                                   |
| [Elapsedtime](../../Shared/CmdLineReference/CmdElapsedTime.html)                   | Enables or disables display of elapsed time for command execution.                                     | <span class="AppCommand">splice&gt; elapsedtime on;</span>                                                                                      |
| [Execute](../../Shared/CmdLineReference/CmdExecute.html)                           | Executes an SQL prepared statement or SQL command string.                                              | <span class="AppCommand">splice&gt; execute 'insert into myTable(id, val) values(?,?)' ;</span>                                                 |
| [Exit](../../Shared/CmdLineReference/CmdExit.html)                                 | Causes the command line interface to exit.                                                             | <span class="AppCommand">splice&gt; exit;</span>                                                                                                |
| [Explain](../../Shared/CmdLineReference/CmdExplainPlan.html)                       | Displays the execution plan for an SQL statement.                                                      | <span class="AppCommand">splice&gt; explain select count(\*) from si;</span>                                                                    |
| [Export](../../Shared/CmdLineReference/CmdExport.html)                             | Exports query results to CSV files.                                                                    | <span class="AppCommand">splice&gt; EXPORT('/my/export/dir', null, null, null, null, null) SELECT a,b,sqrt(c) FROM join t2 on t1.a=t2.a;</span> |
| [Help](../../Shared/CmdLineReference/CmdHelp.html)                                 | Displays a list of the available commands.                                                             | <span class="AppCommand">splice&gt; help;</span>                                                                                                |
| [MaximumDisplayWidth](../../Shared/CmdLineReference/CmdMaxDisplayWidth.html)       | Sets the maximum displayed width for each column of results displayed by the command line interpreter. | <span class="AppCommand">splice&gt; maximumdisplaywidth 30;</span>                                                                              |
| [Prepare](../../Shared/CmdLineReference/CmdPrepare.html)                           | Creates a prepared statement for use by other commands.                                                | <span class="AppCommand">splice&gt; prepare seeMenu as 'SELECT \* FROM menu';</span>                                                            |
| [Release Savepoint](../../Shared/CmdLineReference/CmdReleaseSavepoint.html)        | Releases a savepoint.                                                                                  | <span class="AppCommand">splice&gt; release savepoint gSavePt1;</span>                                                                          |
| [Remove](../../Shared/CmdLineReference/CmdRemove.html)                             | Removes a previously prepared statement.                                                               | <span class="AppCommand">splice&gt; remove seeMenu;</span>                                                                                      |
| [Rollback](../../Shared/CmdLineReference/CmdRollback.html)                         | Rolls back the currently active transaction and initiates a new transaction.                           | <span class="AppCommand">splice&gt; rollback;</span>                                                                                            |
| [Rollback to Savepoint](../../Shared/CmdLineReference/CmdRollbackToSavepoint.html) | Rolls the current transaction back to the specified savepoint.                                         | <span class="AppCommand">splice&gt; rollback to savepoint gSavePt1;</span>                                                                      |
| [Run](../../Shared/CmdLineReference/CmdRun.html)                                   | Runs commands from a file.                                                                             | <span class="AppCommand">splice&gt; run myCmdFile;</span>                                                                                       |
| [Savepoint](../../Shared/CmdLineReference/CmdSavepoint.html)                       | Creates a savepoint within the current transaction.                                                    | <span class="AppCommand">splice&gt; savepoint gSavePt1;</span>                                                                                  |
| [Set Connection](../../Shared/CmdLineReference/CmdSetConnection.html)              | Allows you to specify which connection is the current connection                                       | <span class="AppCommand">splice&gt; set connection sample1;</span>                                                                              |
| [Show](../../Shared/CmdLineReference/ShowCmds.html)                                | Displays information about active connections and database objects.                                    | <span class="AppCommand">splice&gt; show connections;</span>                                                                                    |

 


