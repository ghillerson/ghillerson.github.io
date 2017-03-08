[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/Transactions.html)

[]()Running Transactions In Splice Machine
==========================================

Splice Machine is a fully transactional database that supports ACID transactions. This allows you to perform actions such as <span class="ItalicFont">commit</span> and <span class="ItalicFont">rollback</span>; in a transactional context, this means that the database does not make changes visible to others until a <span class="ItalicFont">commit</span> has been issued.

This topic includes brief overview information about transaction processing with Splice Machine, in these sections:

-   [Transactions Overview](#Transact)
    -   [ACID Transactions](#ACIDTra) describes what ACID transactions are and why they're important.
    -   [MVCC and Snapshot Isolation](#Snapshot) describes what snapshot isolation is and how it works in Splice Machine.
-   [Using Transactions](#Using2)
    -   [Committing and Rolling Back Transaction Changes](#Committi) introduces autocommit, commit, and rollback of transactions.
    -   [A Simple Transaction Example](#Simple) presents an example of a transaction using the <span class="AppCommand">splice&gt;</span> command line interface.
    -   [Using Savepoints](#Using) describes how to use savepoints within transactions.

[]()Transactions Overview
-------------------------

A transaction is a unit of work performed in a database; to maintain the integrity of the database, each transaction must:

-   complete in its entirety or have no effect on the database
-   be isolated from other transactions that are running concurrently in the database
-   produce results that are consistent with existing constraints in the database
-   write its results to durable storage upon successful completion

### []()ACID Transactions

The properties that describe how transactions must maintain integrity are <span class="ItalicFont">A</span>tomicity, <span class="ItalicFont">C</span>onsistency, <span class="ItalicFont">I</span>solation, and <span class="ItalicFont">D</span>urability. Transactions adhering to these properties are often referred to as <span class="ItalicFont">ACID</span> transactions. Here's a summary of ACID transaction properties:

| Property    | Description                                                                                                                                                                                                                                                                                  |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Atomicity   | Requires that each transaction be atomic, i.e. all-or-nothing: if one part of the transaction fails, the entire transaction fails, and the database state is left unchanged. Splice Machine guarantees atomicity in each and every situation, including power failures, errors, and crashes. |
| Consistency | Ensures that any transaction will bring the database from one valid state to another. Splice Machine makes sure that any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof.                  |
| Isolation   | Ensures that the concurrent execution of transactions results in a system state that would be obtained if transactions were executed serially. Splice Machine implements snapshot isolation using MVCC to guarantee that this is true.                                                       |
| Durability  | Ensures that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors. Splice Machine stores changes in durable storage when they are committed.                                                                                        |

### []()[]()MVCC and Snapshot Isolation

Splice Machine employs a lockless <span class="ItalicFont">snapshot isolation design</span> that uses <span class="ItalicFont">Multiple Version Concurrency Control (MVCC)</span> to create a new version of the record every time it is updated and enforce consistency. Database systems use concurrency control systems to manage concurrent access. The simplest control method is to use locks that make sure that the writer is finished before any reader can proceed; however, this approach can be very slow. With snapshot isolation, each transaction has its own virtual snapshot of the database, which means that multiple transactions can operate concurrently without creating deadlock conditions.

When Splice Machine needs to update an item in the database, it doesn't actually overwrite the old data value. Instead, it creates a new version with a new timestamp. Which means that readers have access to the data that was available when they began reading, even if that data has been updated by a writer in the meantime. This is referred to as <span class="ItalicFont">point-in-time consistency</span> and ensures that:

-   Every transaction runs in its own <span class="ItalicFont">transactional context</span>, which includes a snapshot of the database from when the transaction began.
-   Every read made during a transaction will see a consistent snapshot of the database.
-   A transaction can only commit its changes if they do not conflict with updates that have been committed while the transaction was running.

#### Reading and Writing Database Values During a Transaction

When you begin a transaction, you start working within a <span class="ItalicFont">transactional context</span> that includes a snapshot of the database. The operations that read and write database values for your transaction modify your transactional context. When your transaction is complete, you can commit those modifications to the database. The commit of your transaction's changes succeeds unless a <span class="ItalicFont">write-write conflict</span> occurs, which happens when your transaction attempts to commit an update to a value, and another update to that value has already been committed by a transaction that started before your transaction.

This means that the following statements are true with regard to reading values from and writing values to the database during a transaction:

-   When you read a value during a transaction, you get the value that was most recently set within your transactional context. If you've not already set the value within your context, then this is the value that had been most recently committed in the database before your transaction began (and before your transactional context was established).
-   When you write a value during a transaction, the value is set within your transactional context. It is only written to the database when you commit the transaction; that time is referred to as the <span class="ItalicFont">commit timestamp</span> for your transaction. The value changes that you commit then become visible to transactions that start after your transaction's commit timestamp (until another transaction modifies the value).
-   If two parallel transactions attempt to change the same value, then a <span class="ItalicFont">write-write conflict</span> occurs, and the commit of the transaction that started later fails.

#### A Snapshot Isolation Example[]()

The following diagram shows an example of snapshot isolation for a set of transactions, some of which are running in parallel:

<img src="../../../Resources/Images/GS.SnapshotIsolation.png" alt="Snapshot Isolation" class="indented" />

Here's a tabular version of the same transactional timeline, showing the values committed in the database over time, with added commentary:

Time
Committed Values
Transactions
Comments
 
A
B
C
T1
T2
T3
T3'
 
t1
10
20
0
 
 
 
 
 
t2
 
 
 
T1 Start
 
 
 
T1 starts. The starting values within its transactional context are: <span class="CodeFont">A=10, B=20, C=0</span>.
t3
 
 
 
A=A+10
\[A=20\]
 
 
 
T1 modifies the value of <span class="CodeFont">A</span> within its context.
t4
 
 
 
 
T2 Start
 
 
T2 starts. The starting values within its transactional context are the same as for T1: <span class="CodeFont">A=10, B=20, C=0</span>.
t5
 
 
 
A=A+10
\[A=30\]
 
 
 
T1 again modifies the value of <span class="CodeFont">A</span> within its context
t6
30
20
0
Commit
 
 
 
T1 commits its modifications to the database.
t7
 
 
 
 
 
T3 Start
 
T3 starts. The starting values within its transactional context include the commits from T1: <span class="CodeFont">A=30, B=20, C=0</span>.
t8
 
 
 
T1 End
 
 
 
 
t9
 
 
 
 
B=B+10
\[B=30\]
 
 
T2 modifies the value of <span class="CodeFont">B</span> within its context.
t10
 
 
 
 
C=A+10
\[C=20\]
 
 
T2 modifies the value of <span class="CodeFont">C</span> within its context; note that this computation correctly uses the value of <span class="CodeFont">A</span> (<span class="CodeFont">10</span>) that had been committed prior to the start of T2.
t11
30
30
20
 
Commit
 
 
T2 commits its changes.
t12
 
 
 
 
T2 End
 
 
 
t13
 
 
 
 
 
B=B+10
\[B=30\]
 
T3 modifies <span class="CodeFont">B</span>; since its context includes the value of <span class="CodeFont">B</span> before T2 committed, it modifies the original value of B <span class="CodeFont">\[B=20\]</span> in its own context.
t14
 
 
 
 
 
Rollback
 
T3 attempts to commit its changes, which causes a <span class="ItalicFont">write-write conflict</span>, since T2 already committed an update to value <span class="CodeFont">B</span> after T3 started.

T3 rolls back and resets.

t15
 
 
 
 
 
T3 End
 
 
t16
 
 
 
 
 
 
T3' Start
T3 reset (T3') starts. The starting values within its transactional context include the commits from T1 and T2: <span class="CodeFont">A=30, B=30, C=20</span>.
t17
 
 
 
 
 
 
B=B+10
\[B=40\]
T3 modifies the value of <span class="CodeFont">B</span>, which has been updated and committed by T2.
t18
40
40
20
 
 
 
Commit
T3 commits its changes.
t19
 
 
 
 
 
 
T3' End
 
[]()Using Transactions
----------------------

This section describes using transactions in your database, in these subsections:

-   [Committing and Rolling Back Transaction Changes](#Committi) introduces autocommit, commit, and rollback of transactions.
-   [A Simple Transaction Example](#Simple) presents an example of a transaction using the splice&gt; command line interface.
-   [Using Savepoints](#Using) describes how to use savepoints within transactions.
-   [Using Rollback versus Rollback to Savepoint](#Rollbacks) discusses the differences between rolling back a transaction, and rolling back to a savepoint.

### []()Committing and Rolling Back Transaction Changes

Within a transactional context, how the changes that you make are committed to the database depends on whether <span class="CodeFont">autocommit</span> is enabled or disabled:

| <span class="CodeBoldFont">autocommit</span> status | How changes are committed and rolled back                                                            |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------|
| enabled                                             | Changes are automatically committed whenever the operation completes successfully.                   
                                                                                                                                                             
                                                       If an operation reports any error, the changes are automatically rolled back.                         |
| disabled                                            | Changes are only committed when you explicitly issue a <span class="CodeFont">commit</span> command. 
                                                                                                                                                             
                                                       Changes are rolled back when you explicitly issue a <span class="CodeFont">rollback</span> command.   |

Autocommit is enabled by default. You typically disable <span class="CodeFont">autocommit</span> when you want a block of operations to be committed atomically (all at once) instead of committing changes to the database after each operation.

You can turn <span class="CodeFont">autocommit</span> on and off by issuing the <span class="CodeFont">autocommit on</span> or <span class="CodeFont">autocommit off</span> commands at the <span class="CodeFont">splice&gt;</span> prompt.

For more information, see these topics in the <span class="ItalicFont">[Command Line Reference](../../CmdLineReference/Intro.CmdLineReference.html)</span> section of this book:

-   <span class="CodeFont">[autocommit](../../CmdLineReference/CmdAutocommit.html)</span> command
-   <span class="CodeFont">[commit](../../CmdLineReference/CmdCommit.html)</span> command
-   <span class="CodeFont">[rollback](../../CmdLineReference/CmdRollback.html)</span> command

### []()A Simple Transaction Example

Here is a simple example. Enter the following commands to see <span class="ItalicFont">commit</span> and <span class="ItalicFont">rollback</span> in action:

``` AppCommand
splice> create table myTbl (i int);
splice> autocommit off;                  - commits must be made explicitly
splice> insert into myTbl  values 1,2,3; - inserted but not visible to others
splice> commit;                          - now committed to the database
splice> select * from myTbl;             - verify table contents
splice> insert into myTbl  values 4,5;   - insert more data
splice> select * from myTbl;             - verify table contents
splice> rollback;                        - roll back latest insertions
splice> select * from myTbl;             - and verify again
... 
```

You can turn <span class="CodeFont">autocommit</span> back on by issuing the command: <span class="AppCommand">autocommit on;</span>

### []()Using Savepoints

Splice Machine supports the JDBC 3.0 Savepoint API, which adds methods for setting, releasing, and rolling back to savepoints within a transaction. Savepoints give you additional control over transactions by allowing you to define logical rollback points within a transaction, which effectively allows you to specify sub-transactions (also known as nested transactions).

You can specify multiple savepoints within a transaction. Savepoints are very useful when processing large transactions: you can implement error recovery schemes that allow you to rollback part of a transaction without having to abort the entire transaction.

You can use these commands to work with Savepoints:

-   create a savepoint with the <span class="CodeFont">savepoint</span> command
-   release a savepoint with the <span class="CodeFont">release savepoint</span> command
-   roll a transaction back to an earlier savepoint with the <span class="CodeFont">rollback to savepoint</span> command

#### Example

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

### []()Using Rollback Versus Rollback to Savepoint

There's one important distinction you should be aware of between rolling back to a savepoint versus rolling back the entire transaction:

-   When you perform a <span class="CodeFont">rollback</span>, Splice Machine aborts the entire transaction and creates a new transaction,
-   When you perform a <span class="CodeFont">rollback to savepoint</span>, Splice Machine rolls back part of the changes, but does not create a new transaction.

Remember that this distinction also holds in a multi-tenant environment. In other words:

-   If two users are making modifications to the same table in separate transactions, and one user does a <span class="CodeFont">rollback</span>, all changes made by that user prior to that rollback are no longer in the database.
-   Similarly, if two users are making modifications to the same table in separate transactions, and one user does a <span class="CodeFont">rollback to savepoint</span>, all changes made by that user since the savepoint was established are no longer in the database.

See Also
--------

-   <span class="CodeFont">[autocommit](../../CmdLineReference/CmdAutocommit.html)</span> command
-   <span class="CodeFont">[commit](../../CmdLineReference/CmdCommit.html)</span> command
-   <span class="CodeFont">[release savepoint](../../CmdLineReference/CmdReleaseSavepoint.html)</span> command
-   <span class="CodeFont">[rollback](../../CmdLineReference/CmdRollback.html)</span> command
-   <span class="CodeFont">[rollback to savepoint](../../CmdLineReference/CmdRollbackToSavepoint.html)</span> command
-   <span class="CodeFont">[savepoint](../../CmdLineReference/CmdSavepoint.html)</span> command

 


