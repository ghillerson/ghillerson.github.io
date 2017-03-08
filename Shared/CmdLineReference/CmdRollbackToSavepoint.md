[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdRollbackToSavepoint.html)

[]()Rollback to Savepoint Command
=================================

The <span class="AppCommand">rollback to savepoint</span> command issues a <span class="CodeFont">java.sql.Connection.rollback</span> request, which has been overloaded to work with a savepoint within the current transaction.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When you rollback a transaction to a savepoint, that savepoint and any others created after it within the transaction are automatically released.

Syntax

``` FcnSyntax
rollback to savepoint identifier;
```

<span class="ItalicFont">identifier</span>

The name of the savepoint to which the transaction should be rolled back: all savepoints up to and including this one are rolled back.

Usage Notes

In contrast to the <span class="CodeFont">[Rollback](CmdRollback.html)</span> command, the <span class="CodeFont">Rollback to Savepoint</span> command rolls back but of your work, but does not start a new transaction.

Examples

First we'll create a table, turn autocommit off, and insert some data into the table. We then create a savepoint, and verify the contents of our table:

``` AppCommand
splice> CREATE TABLE myTbl(i int);
0 rows inserted/updated/deleted
splice> AUTOCOMMIT OFF;
splice> INSERT INTO myTbl VALUES 1,2,3;
3 rows inserted/updated/deleted
splice> SAVEPOINT savept1;
0 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          

3 rows selected
```

Next we add new values to the table and again verify its contents:

``` AppCommand
splice> INSERT INTO myTbl VALUES 4,5;
2 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          
4          
5


5 rows selected
```

Now we roll back to our savepoint, and verify that the rollback worked:

``` AppCommand
splice> ROLLBACK TO SAVEPOINT savept1;
0 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          

3 rows selected
```

And finally, we commit the transaction:

``` AppCommand
COMMIT;
```

See Also

-   [savepoint](CmdSavepoint.html) command
-   [release savepoint](CmdReleaseSavepoint.html) command
-   The <span class="ItalicFont">[Running Transactions](../Developers/Fundamentals/Transactions.html)</span> topic contains includes a discussion of using savepoints.

 


