[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdPrepare.html)

[]()Prepare Command
===================

The <span class="AppCommand">prepare</span> command creates a <span class="CodeFont">java.sql.PreparedStatement</span> using the value of the specified SQL command <span class="ItalicFont">String</span>, and assigns an identifier to the prepared statement so that other <span class="AppCommand">splice&gt;</span> commands can use the statement.

If a prepared statement with the specified <span class="ItalicFont">Identifier</span> name already exists in the command interpreter, an error is returned, and the previous prepared statement is left unchanged. If there are any errors in preparing the statement, no prepared statement is created.

If the <span class="ItalicFont">Identifier</span> specifies a connection Name, the statement is prepared on the specified connection.

Syntax

``` FcnSyntax
PREPARE Identifier AS String
```

Identifier

The identifier to assign to the prepared statement.

String

The command string to prepare.

Examples

``` AppCommand
splice> prepare seeMenu as 'SELECT * FROM menu';
splice> execute seeMenu;
COURSE    |ITEM                |PRICE          
-----------------------------------------------
entree    |lamb chop           |14             
dessert   |creme brulee        |6

splice> prepare addYears as 'update children set age = age + ? where name = ?';
splice> execute addYears using 'values (10, ''Abigail'')';
```

 


