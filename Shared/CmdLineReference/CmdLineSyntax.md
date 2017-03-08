[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdLineSyntax.html)

[]()Using the splice&gt; Command Line Interface
===============================================

This topic presents information that will help you in using the Splice Machine <span class="AppCommand">splice&gt;</span> command line interpreter, in the following sections:

-   The <a href="#splice%3E" class="selected">splice&gt; Command Line Interpreter</a> section shows you how to invoke the splice&gt; command line.
-   The <a href="#Command" class="selected">Command Line Output</a> section describes how you can adjust the appearance of output from the interepreter.
-   The <a href="#Syntax" class="selected">Command Line Syntax</a> section summarizes the syntax of commands, including capitalization and case-sensitivity rules, as well as various special characters you can use in your commands. It also shows you how to include comments in your command lines and how to run a file of SQL commands.
-   The <a href="#ExampleCommands" class="selected">Example Command Lines</a> section shows several examples of command lines.
-   The [Scripting Splice Commands](CmdLineSummary.html) section describes how to create a script of <span class="AppCommand">splice&gt;</span> commands to run a series of operations like loading a number of files into your database

The remainder of this section contains a reference page for each of the command line commands.

[]()splice&gt; Command Line Interpreter
---------------------------------------

To run the Splice Machine command line interpreter, run the <span class="ShellCommand">sqlshell.sh</span> script in your terminal window.

``` ShellCommand
% ./sqlshell.sh
splice> 
```

When the interpreter prompts you with <span class="AppCommand">splice&gt;</span>, you can enter commands, ending each with a semicolon. For a complete description of <span class="AppCommand">splice&gt;</span> syntax, see the next section in this topic, <a href="#Syntax" class="selected">Command Line Syntax</a>,

Note that you can optionally specify a file of sql commands that the interpreter will run using the <span class="CodeFont">-f</span> parameter; after running those commands, the interpreter exits. For example:

``` ShellCommand
./sqlshell.sh -f /home/mydir/sql/test.sql
```

You can optionally include parameter values when running <span class="ShellCommand">sqlshell.sh</span> script, to change default values. Here's the syntax:

``` ShellCommand
sqlshell.sh [-h host] [-p port ] [-u username] [-s password] [-f commandsFile
```

-host

The hostname or IP address of your Splice Machine HBase RegionServer.

The default value is <span class="CodeFont">localhost</span>.

-port

The port on which Splice Machine is listening for your connection.

The default value is <span class="CodeFont">1527</span>.

-username

The user name for your Splice Machine database.

The default value is <span class="CodeFont">splice</span>.

-password

The password for your Splice Machine database.

The default value is <span class="CodeFont">admin</span>.

-f \[fileName\]

The name of a file with SQL commands in it: <span class="CodeFont">sqlshell</span> starts up the <span class="AppCommand">splice&gt;</span> command line interpreter, runs the commands in the file, and then exits. For example:

``` ShellCommand
$ ./sqlshell.sh -f /home/mydir/sql/test.sql

 ========= rlwrap detected and enabled.  Use up and down arrow keys to scroll through command line history. ======== 

Running Splice Machine SQL shell
For help: "splice> help;"
SPLICE* -   jdbc:splice://10.1.1.111:1527/splicedb
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

The <span class="CodeFont">test.sql</span> file used in the above example contains the following commands:

``` ShellCommand
elapsedtime on;
select count(*) from CUST_EMAIL;
```

[]()[]()Command Line Output
---------------------------

Output from <span class="AppCommand">splice&gt;</span> commands is displayed in your terminal window. The <span class="CodeFont">[maximumdisplaywidth](CmdMaxDisplayWidth.html)</span> setting affects how the output is displayed; specifically, it determines if the content of each column is truncated to fit within the width that you specify.

When you set <span class="CodeFont">[maximumdisplaywidth](CmdMaxDisplayWidth.html)</span> to <span class="CodeFont">0</span>, all output is displayed, without truncation.

[]()Command Line Syntax[]()
---------------------------

This section briefly summarizes the syntax of command lines you can enter in response to the <span class="AppCommand">splice&gt;</span> prompt, including these subsections:

-   <a href="#Finish" class="selected">Finishing and submitting command lines</a>
-   <a href="#Capitali" class="selected">Capitalization and case sensitivity rules</a>
-   <a href="#Special" class="selected">Special character usage</a>
-   <a href="#Multiline" class="selected">Running multi-line commands</a>
-   <a href="#RunFromFile" class="selected">Running commands from a file</a>
-   <a href="#Comments" class="selected">Including comments in your command lines</a>
-   <a href="#Using" class="selected">Using rlWrap on the command line</a>

### []()Finish Commands with a Semicolon

The command line interface allows you to enter multi-line commands, and waits for a non-escaped semicolon (<span class="CodeFont">;</span>) character to signal the end of the command.

A command is not executed until you enter the semicolon character and press the <span class="CodeFont">Return</span> or <span class="CodeFont">Enter</span> key.

### []()[]()Capitalization and Case Sensitivity Rules

Certain identifiers and keywords are case sensitive:

| Identifier             | Case Sensitive?       | Notes and Example                                                                      |
|------------------------|-----------------------|----------------------------------------------------------------------------------------|
| SQL keywords           | Not case sensitive    | These are all equivalent: <span class="Example">SELECT, Select, select, SeLeCt</span>. |
| ANSI SQL identifiers   | Not case sensitive    | These are not case sensitive unless they are delimited.                                |
| Java-style identifiers | Always case sensitive | These are NOT equivalent: <span class="Example">my\_name, My\_Name</span>.             |

### []()[]()Special Characters You Can Use

The following table describes the special characters you can use in commands:

| Purpose                                                                                                  | Character(s) to use                                                     | Notes and example                                                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| To delimit special identifiers                                                                           | Double quotation marks (<span class="CodeFont">"</span>)                | Special identifiers are also known as <span class="ItalicFont">delimited identifiers</span>.                                                                                        |
| To delimit character strings                                                                             | Single quotation marks (<span class="CodeFont">'</span>)                |                                                                                                                                                                                     |
| To escape a single quote or apostrophe within a character string                                         | Single quotation mark ( (<span class="CodeFont">'</span>)               | Since single quotation marks are used to delimit strings, you must escape any single quotation marks you want included in the string itself.                                        
                                                                                                                                                                                                                                                                                                                                                                           
                                                                                                                                                                                      Use the single quotation mark itself as the escape character, which means that you enter two single quotation marks within a character string to include one single quotation mark.  
                                                                                                                                                                                                                                                                                                                                                                           
                                                                                                                                                                                      Example: <span class="Example">'This string includes ''my quoted string'' within it.'</span>                                                                                         |
| To escape a double quote                                                                                 | <span class="ItalicFont">Not needed </span>                             | You can simply include a double quotation mark in your command lines.                                                                                                               |
| To specify a wild card within a Select expression                                                        | The asterisk (<span class="CodeFont">\*</span>) character               | This is the SQL metasymbol for selecting all matching entries.                                                                                                                      
                                                                                                                                                                                                                                                                                                                                                                           
                                                                                                                                                                                      Example: <span class="Example">SELECT \* FROM MyTable;</span>                                                                                                                        |
| To specify a wild card sequence in a string with the <span class="CodeFont">LIKE</span> operator         | The percentage (<span class="CodeFont">%</span>) character              | Example: <span class="Example">SELECT \* FROM MyTable WHERE Name LIKE 'Ga%';</span>                                                                                                 |
| To specify a single wild card character in a string with the <span class="CodeFont">LIKE</span> operator | The underline (<span class="CodeFont">\_</span>) character              | Example: <span class="Example">SELECT \* FROM MyTable WHERE Name LIKE '%Er\_n%';</span>                                                                                             |
| To begin a single-line comment                                                                           | Two dashes (<span class="CodeFont">--</span>)                           | <span class="Example"> -- the following selects everything in my table:</span>                                                                                                      
                                                                                                                                                                                      <span class="Example">SELECT \* FROM MyTable;</span>                                                                                                                                 |
| To bracket a multi-line comment                                                                          | <span class="CodeFont">/\*</span> and <span class="CodeFont">\*/</span> | All text between the comment start <span class="CodeFont">/\*</span> and the comment end <span class="CodeFont">\*/</span> is ignored.                                              
                                                                                                                                                                                                                                                                                                                                                                           
                                                                                                                                                                                      ``` ExampleCell                                                                                                                                                                      
                                                                                                                                                                                      /* the following selects everything in my table,                                                                                                                                     
                                                                                                                                                                                         which we'll then display on the screen */                                                                                                                                         
                                                                                                                                                                                      SELECT * FROM MyTable;                                                                                                                                                               
                                                                                                                                                                                      ```                                                                                                                                                                                  |

### []()Entering Multi-line Commands[]()

When using the command line (the <span class="AppCommand">splice&gt;</span> prompt), you must end each SQL statement with a semicolon (<span class="CodeFont">;</span>). For example:

``` AppCommand
splice> select * from myTable;   
```

You can extend SQL statements across multiple lines, as long as you end the last line with a semicolon. Note that the <span class="CodeFont">splice&gt;</span> command line interface prompts you with a fresh <span class="AppCommand">&gt;</span> at the beginning of each line. For example:

``` AppCommand
splice> select * from myTable
> where i > 1;  
```

### []()Running SQL Statements From a File[]()

You can also create a file that contains a collection of SQL statements, and then use the <span class="CodeFont">run </span>command to run those statements. For example:

``` AppCommand
splice> run 'path/to/file.sql';
```

### []()Including Comments[]()

You can include comments on the command line or in a SQL statement file by prefacing the command with two dashes (<span class="CodeFont">--</span>). Any text following the dashes is ignored by the SQL parser. For example:

``` AppCommand
splice> select * from myTable   -- This selects everything in myTable;
```

### Misaligned Quotes

If you mistakenly enter a command line that has misaligned quotation symbols, the interpreter can seem unresponsive. The solution is to add the missing quotation mark(s), followed by a semicolon, and resubmit the line. It won't work as expected, but it will enable you to keep working.

### []()Using rlWrap on the Command Line&gt;

rlWrap is a Unix utility that Splice Machine encourages you to use: it allows you to scroll through your command line history, reuse and alter lines, and more. We've included a [synopsis of it here.](RLWrapSummary.html)

[]()Example Command Lines[]()
-----------------------------

Here are several example command lines:

Operation
Command Example
Display a list of all tables and their schemas
<span class="AppCommand">splice&gt; show tables;</span>
Display the columns and attributes of a table
<span class="AppCommand">splice&gt; describe tableA;</span>
Limit the number of rows returned from a select statement
<span class="AppCommand">splice&gt; select \* from tableA { limit 10 };</span>
Print a current time stamp
<span class="AppCommand">splice&gt; values current\_timestamp;</span>
<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Remember that you must end your command lines with the semicolon (<span class="CodeFont">;</span>) character, which submits the command line to the interpreter.

[]()Scripting <span class="AppCommand">splice&gt;</span> Commands
-----------------------------------------------------------------

You can use the Splice Machine Command Line Interface (<span class="AppCommand">splice&gt;</span>) to interactively run database commands. This topic describes how to create a script of <span class="AppCommand">splice&gt;</span> commands to run a series of operations, such as loading a number of files into your database. To script a series of <span class="AppCommand">splice&gt;</span> commands, you need to create:

-   an SQL commands file containing the SQL statements you want executed
-   an SQL file to connect to the database and invoke the SQL commands file
-   a shell script using Bash (<span class="CodeFont">/bin/bash</span>)

Follow these steps to create your script:

1.  Create a file of SQL commands:

    First, create a file that contains the SQL commands you want to run against your Splice Machine database. For this example, we'll create a file named <span class="CodeFont">create-my-tables.sql</span> that creates a table in the database:

    ``` Example
    create table customers (
       CUSTOMER_ID BIGINT,
       FIRST_NAME VARCHAR(30),
       LAST_NAME VARCHAR(30)
    );
    ```

2.  Create an SQL file to connect to the database and invoke the commands file

    We need a separate SQL file named <span class="CodeFont">my\_load\_datascript.sql</span>that connects to your database and then invokes the file of SQL commands we just created.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The <span class="CodeFont">connect</span> command in this file must run before running the file of SQL statements.

    Here we name the first SQL file, and define it to run the SQL statements file named <span class="CodeFont">create-my-tables.sql:</span>

    ``` Example
       --First connect to the database
    connect 'jdbc:splice://<regionServer>:1527/splicedb';

       --Next run your sql file
    run '/users/yourname/create-my-tables.sql';

    show tables;
    quit;
    ```

    If you are running Splice Machine on a cluster, connect from a machine that is NOT running an HBase RegionServer and specify the IP address of a <span class="HighlightedCode">regionServer</span> node, e.g. <span class="AppCommand">10.1.1.110</span>. If you're using the standalone version of Splice Machine, specify <span class="HighlightedCode">localhost</span> instead.

3.  Create a shell script to run your SQL connect file

    We now create a shell script named <span class="CodeFont">load\_datascript.sh</span> to run the <span class="CodeFont">my\_load\_datascript.sql</span> file:

    ``` Example
    #!/bin/bash

    export CLASSPATH=<FULL_PATH_TO_SPLICEMACHINE_JAR_FILE>
    java -Djdbc.drivers=com.splicemachine.db.jdbc.ClientDriver -Dij.outfile=my_load_datascript.out com.splicemachine.db.tools.ij < my_load_datascript.sql
    ```

    The first line of this script must set the <span class="CodeFont">CLASSPATH</span> to the location of your Splice Machine jar file. The second line runs the ij command, specifying its output file (<span class="CodeFont">my\_load\_datascript.out</span>) and its SQL commands input file, which is the <span class="CodeFont">my\_load\_datascript\_sql</span> file that we created in the previous step.

4.  Make your shell script executable

    We need to make the shell script executable with the chmod shell command:

    ``` ShellCommand
    chmod +x load_datascript.sh
    ```

5.  Use nohup to run the script

    The <span class="ShellCommand">nohup</span> utility allows you to run a script file in the background, which means that it will continue running if you log out, disconnect from a remote machine, or lose your network connection.

    ``` ShellCommand
    nohup ./load_datascript.sh > ./load_datascript.out 2>&1 &
    ```

    Here's the syntax for the <span class="CodeFont">nohup</span> utility:

    ``` FcnSyntax
    nohup ./command-name.sh > ./command-name.out 2>&1 &
    ```

    command-name.sh

    The name of the shell script or a command name.

    command-name.out

    The name of the file to capture any output written to <span class="CodeFont">stdout</span>.

    2&gt;&1

    This causes <span class="CodeFont">stderr</span> (file descriptor <span class="CodeFont">2</span>) to be written to <span class="CodeFont">stdout</span> (file descriptor <span class="CodeFont">1</span>); this means that all output will be captured in <span class="CodeFont">command-name.out</span>.

    &

    The <span class="ShellCommand">nohup</span> utility does not automatically run its command in the background, so we add the <span class="CodeFont">&</span> to do

 


