[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdExecute.html)

[]()Execute Command
===================

The <span class="AppCommand">execute</span> command executes an SQL command string or a prepared statement.

Syntax

``` FcnSyntax
EXECUTE { SQLString | PreparedStatementIdentifier }
[ USING { String | Identifier } ]
```

SQLString

The SQL command string to execute; this string is passed to the connection without further processing by the command line interpreter.

PreparedStatementIdentifier

The identifier of the prepared statement to execute; this must be the name associated with a prepared statement when created by the [Prepare](CmdPrepare.html) command.

String

Use this or <span class="ItalicFont">Identifier</span> to supply values for dynamic parameters, if the command being executed contains them.

Identifier

Use this or <span class="ItalicFont">String</span> to supply values for dynamic parameters, if the command being executed contains them. This identifier must have a result set as its result:

-   Each row of the result set is applied to the input parameters of the command to be executed, so the number of columns in the <span class="CodeFont">Using</span> clause's result set must match the number of input parameters in the statement being executed.
-   The command line interpreter displays the results of each execution of the statement as they are created.
-   If the Using clause's result set contains zero rows, the statement is not executed.

Examples

``` AppCommand
splice> autocommit off;
splice> prepare menuInsert as 'INSERT INTO menu VALUES (?, ?, ?)';
splice> execute menuInsert using 'VALUES
(''entree'', ''lamb chop'', 14),
(''dessert'', ''creme brulee'', 6)';
1 row inserted/updated/deleted
1 row inserted/updated/deleted
splice> commit; 
splice> connect 'jdbc:splice://abc:1527/splicedb;user=me;password=mypswd';
splice> create table firsttable (id int primary key,
name varchar(12));
0 rows inserted/updated/deleted
splice> insert into firsttable values 
10,'TEN'),(20,'TWENTY'),(30,'THIRTY');
3 rows inserted/updated/deleted
splice> select * from firsttable;
ID         |NAME        
------------------------
10         |TEN         
20         |TWENTY      
30         |THIRTY      

3 rows selected
splice> connect 'jdbc:splice://xyz:1527/splicedb';
splice(CONNECTION1)> create table newtable (newid int primary key, 
newname varchar(12));
0 rows inserted/updated/deleted
splice(CONNECTION1)> prepare src@connection0 as 'select * from firsttable';
splice(CONNECTION1)> autocommit off;
splice(CONNECTION1)> execute 'insert into newtable(newid, newname) 
values(?,?)' using src@connection0;
1 row inserted/updated/deleted
1 row inserted/updated/deleted
1 row inserted/updated/deleted
splice(CONNECTION1)> commit;
splice(CONNECTION1)> select * from newtable;
NEWID      |NEWNAME     
------------------------
10         |TEN         
20         |TWENTY      
30         |THIRTY      

3 rows selected
splice(CONNECTION1)> show connections;
CONNECTION0 -   jdbc:splice://abc:1527/splicedb
CONNECTION1* -  jdbc:splice://xyz:1527/splicedb
splice(CONNECTION1)> disconnect connection0;
splice> 
```

 


