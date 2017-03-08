[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdAutocommit.html)

[]()Autocommit Command
======================

The <span class="AppCommand">autocommit</span> command enables or disables auto-commit mode.

JDBC specifies that the default auto-commit mode is enabled; however, certain types of processing require that auto-commit mode be disabled.

Syntax

``` FcnSyntax
AUTOCOMMIT {ON | OFF}
```

ON

Enables auto-commit mode.

If auto-commit mode is changed from disabled (<span class="CodeFont">off</span>) to enabled (<span class="CodeFont">on</span>) when there is a transaction outstanding, that work is committed when the current transaction commits, not at the time auto-commit is enabled. Thus, if you are enabling auto-commit when a transaction is outstanding, first use either the [Commit](CmdCommit.html) command or the [Rollback](CmdRollback.html) command to ensure that all prior work is completed before the return to auto-commit mode.

OFF

Disables auto-commit mode.

Examples

``` AppCommand
splice> autocommit off;
splice> DROP TABLE menu;
0 rows inserted/updated/deleted 
splice> CREATE TABLE menu (course CHAR(10), item CHAR(20), price INT);
0 rows inserted/updated/deleted
splice> INSERT INTO menu VALUES ('entree', 'lamb chop', 14),
('dessert', 'creme brulee', 6), 
('appetizer', 'baby greens', 7);
3 rows inserted/updated/deleted
splice> commit;
splice> autocommit on;
splice>
```

 


