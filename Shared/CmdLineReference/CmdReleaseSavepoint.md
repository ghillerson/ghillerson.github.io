[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdReleaseSavepoint.html)

[]()Release Savepoint Command
=============================

The <span class="AppCommand">release savepoint</span> command issues a <span class="CodeFont">java.sql.Connection.releaseSavepoint</span> request, which releases a savepoint within the current transaction. Once a savepoint has been released, attempting to reference it in a rollback operation will cause an <span class="CodeFont">SQLException</span> to be thrown.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When you commit a transaction, any savepoints created in that transaction are automatically released and invalidated when the transaction is committed or the entire transaction is rolled back.
When you rollback a transaction to a savepoint, that savepoint and any others created after it within the transaction are automatically released.

Syntax

``` FcnSyntax
release savepoint identifier;
```

<span class="ItalicFont">identifier</span>

The name of the savepoint to release.

Examples

#### Example

First we'll create a table, turn <span class="CodeFont">autocommit</span> off, and insert some data into the table. We then create a savepoint, and verify the contents of our table:

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

Now we release our original savepoint, insert a few more values, and create a new savepoint, <span class="CodeFont">savept2</span>.

``` AppCommand
splice> RELEASE SAVEPOINT savept1;
0 rows inserted/updated/deleted
splice> INSERT INTO myTbl VALUES 6,7;
2 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          
4        
5        
6        
7

7 rows selected
splice> SAVEPOINT savept2;
0 rows inserted/updated/deleted
```

We again insert data into the table, display its contents, and then do a rollback:

``` AppCommand
splice> INSERT INTO myTbl VALUES 8,9;
2 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          
4          
5          
6          
7          
8          
9          

9 rows selected
splice> ROLLBACK TO SAVEPOINT savept1;
ERROR 3B001: Savepoint SAVEPT1 does not  exist or is not active in the current transaction.
splice> ROLLBACK TO SAVEPOINT savept2;
0 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
I          
-----------
1          
2          
3          
4          
5          
6          
7          

7 rows selected
```

And finally, we commit the transaction:

``` AppCommand
COMMIT;
```

See Also

-   [savepoint](CmdSavepoint.html) command
-   [rollback to savepoint](CmdRollbackToSavepoint.html) command
-   The <span class="ItalicFont">[Running Transactions](../Developers/Fundamentals/Transactions.html)</span> topic contains includes a discussion of using savepoints.

 


