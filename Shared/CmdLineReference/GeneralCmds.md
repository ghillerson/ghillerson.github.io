[Open topic with navigation](../../index.html#Shared/CmdLineReference/GeneralCmds.html)

[]()General Commands
====================

This section describes the general-purpose <span class="AppCommand">splice&gt;</span> commands:

| Command                                        | Description                                                                                            | Usage                                                                                                                                           |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| [Describe](CmdDescribe.html)                   | Displays a description of a table or view.                                                             | <span class="AppCommand">splice&gt; describe myTable;</span>                                                                                    |
| [Elapsedtime](CmdElapsedTime.html)             | Enables or disables display of elapsed time for command execution.                                     | <span class="AppCommand">splice&gt; elapsedtime on;</span>                                                                                      |
| [Execute](CmdExecute.html)                     | Executes an SQL prepared statement or SQL command string.                                              | <span class="AppCommand">splice&gt; execute 'insert into myTable(id, val) values(?,?)' ;</span>                                                 |
| [Exit](CmdExit.html)                           | Causes the command line interface to exit.                                                             | <span class="AppCommand">splice&gt; exit;</span>                                                                                                |
| [Export](CmdExport.html)                       | Exports query results to CSV files.                                                                    | <span class="AppCommand">splice&gt; EXPORT('/my/export/dir', null, null, null, null, null) SELECT a,b,sqrt(c) FROM join t2 on t1.a=t2.a;</span> |
| [Help](CmdHelp.html)                           | Displays a list of the available commands.                                                             | <span class="AppCommand">splice&gt; help;</span>                                                                                                |
| [MaximumDisplayWidth](CmdMaxDisplayWidth.html) | Sets the maximum displayed width for each column of results displayed by the command line interpreter. | <span class="AppCommand">splice&gt; maximumdisplaywidth 30;</span>                                                                              |
| [Prepare](CmdPrepare.html)                     | Creates a prepared statement for use by other commands.                                                | <span class="AppCommand">splice&gt; prepare seeMenu as 'SELECT \* FROM menu';</span>                                                            |
| [Remove](CmdRemove.html)                       | Removes a previously prepared statement.                                                               | <span class="AppCommand">splice&gt; remove seeMenu;</span>                                                                                      |
| [Run](CmdRun.html)                             | Runs commands from a file.                                                                             | <span class="AppCommand">splice&gt; run myCmdFile;</span>                                                                                       |

 


