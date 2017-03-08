[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdSavepoint.html)

[]()Savepoint Command
=====================

The <span class="AppCommand">savepoint</span> command issues a <span class="CodeFont">java.sql.Connection.setSavepoint</span> request, which sets a savepoint within the current transaction.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Savepoints are only useful when autocommit is off.
You can define multiple savepoints within a transaction.

Syntax

``` FcnSyntax
savepoint identifier;
```

<span class="ItalicFont">identifier</span>

An identifier name for the string.

Example

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

-   [release savepoint](CmdReleaseSavepoint.html) command
-   [rollback to savepoint](CmdRollbackToSavepoint.html) command
-   The <span class="ItalicFont">[Running Transactions](../Developers/Fundamentals/Transactions.html)</span> topic contains includes a discussion of using savepoints.

 


