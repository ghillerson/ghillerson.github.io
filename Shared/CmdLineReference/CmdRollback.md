[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdRollback.html)

[]()Rollback Command
====================

The <span class="AppCommand">rollback</span> command issues a <span class="CodeFont">java.sql.Connection.rollback</span> request, which rolls back (undoes) the currently active transaction and initiates a new transaction.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You should only use this command when auto-commit mode is disabled.

Usage Notes

In contrast to the <span class="CodeFont">[Rollback to Savepoint](CmdRollbackToSavepoint.html)</span> command, the <span class="CodeFont">Rollback</span> command aborts the current transaction and starts a new one.

Examples

``` AppCommand
splice> autocommit off;
splice> INSERT INTO menu VALUES ('dessert', 'rhubarb pie', 4);
1 row inserted/updated/deleted
splice> SELECT * from menu;
COURSE    |ITEM                |PRICE
-----------------------------------------------
entree    |lamb chop           |14
dessert   |creme brulee        |7
appetizer |baby greens         |7
dessert   |rhubarb pie         |4

4 rows selected
splice> rollback;
splice> SELECT * FROM menu;
COURSE    |ITEM                |PRICE
-----------------------------------------------
entree    |lamb chop           |14
dessert   |creme brulee        |7
appetizer |baby greens         |7

3 rows selected
splice>
```

 


