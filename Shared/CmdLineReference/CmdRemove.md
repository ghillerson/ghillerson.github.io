[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdRemove.html)

[]()Remove Command
==================

The <span class="AppCommand">remove</span> command removes a previously prepared statement from the command line interpreter.

The statement is closed, releasing its database resources.

Syntax

``` FcnSyntax
REMOVE Identifier
```

Identifier

The name assigned to the prepared statement when it was prepared with the [Prepare](CmdPrepare.html) statement.

Examples

``` AppCommand
splice> prepare seeMenu as 'SELECT * FROM menu';
splice> execute seeMenu;
COURSE    |ITEM                |PRICE          
-----------------------------------------------
entree    |lamb chop           |14             
dessert   |creme brulee        |6

2 rows selected
splice> remove seeMenu;
splice> execute seeMenu;
splice ERROR: Unable to establish prepared statement SEEMENU
splice>
```

 


