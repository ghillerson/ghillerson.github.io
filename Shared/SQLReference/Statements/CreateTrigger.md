[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateTrigger.html)

<a href="" id="Statements.CreateTrigger"></a>[]()CREATE TRIGGER
===============================================================

A <span class="CodeFont">CREATE TRIGGER</span> statement creates a trigger, which defines a set of actions that are executed when a database event known as the <span class="CodeFont">triggering event</span> occurs on a specified table. The event can be a <span class="CodeFont">INSERT</span>, <span class="CodeFont">UPDATE</span>, or <span class="CodeFont">DELETE</span> statement. When a trigger fires, the set of SQL statements that constitute the action are executed.

You can define any number of triggers for a single table, including multiple triggers on the same table for the same event. To define a trigger on a table, you must be the owner of the of the database, the owner of the table's schema, or have <span class="CodeFont">TRIGGER</span> privileges on the table. You cannot define a trigger for any schema whose name begins with <span class="CodeFont">SYS</span>.

The [Database Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) topic in our <span class="ItalicFont">Developer's Guide</span> provides additional information about database triggers.

Syntax

``` FcnSyntax
CREATE TRIGGER TriggerName 
   { AFTER | BEFORE }  
   { INSERT | DELETE | UPDATE [ OF column-Name [, column-Name]* ] }
   ON table-Name
      [ ReferencingClause ]
      [ FOR EACH { ROW | STATEMENT } ]
 Triggered-SQL-statement
```

TriggerName

The name to associate with the trigger.

AFTER | BEFORE

Triggers are defined as either <span class="ItalicFont">Before</span> or <span class="ItalicFont">After</span> triggers.

<span class="CodeFont">BEFORE</span> triggers fire before the statement's changes are applied and before any constraints have been applied. <span class="CodeFont">AFTER</span> triggers fire after all constraints have been satisfied and after the changes have been applied to the target table.

When a database event occurs that fires a trigger, Splice Machine performs actions in this order:

-   It fires <span class="CodeFont">BEFORE</span> triggers.
-   It performs constraint checking (primary key, unique key, foreign key, check).
-   It performs the <span class="CodeFont">INSERT</span>, <span class="CodeFont">UPDATE</span>, <span class="CodeFont">SELECT</span>, or <span class="CodeFont">DELETE</span> operations.
-   It fires <span class="CodeFont">AFTER</span> triggers.

When multiple triggers are defined for the same database event for the same table for the same trigger time (before or after), triggers are fired in the order in which they were created.

INSERT | DELETE | SELECT | UPDATE

Defines which database event causes the trigger to fire. If you specify <span class="CodeFont">UPDATE</span>, you can specify which column(s) cause the triggering event.

table-Name

The name of the table for which the trigger is being defined.

ReferencingClause

A means of referring to old/new data that is currently being changed by the database event that caused the trigger to fire. See the [Referencing Clause](#ReferencingClause) section below.

FOR EACH {ROW | STATEMENT}

A <span class="CodeFont">FOR EACH ROW</span> triggered action executes once for each row that the triggering statement affects.

A <span class="CodeFont">FOR EACH STATEMENT</span> trigger fires once per triggering event and regardless of whether any rows are modified by the insert, update, or delete event.

Triggered-SQL-Statement

The statement that is executed when the trigger fires. The statement has the following restrictions:

-   It must not contain any dynamic (<span class="CodeFont">?</span>) parameters.
-   It cannot create, alter, or drop any table.
-   It cannot add an index to or remove an index from any table.
-   It cannot add a trigger to or drop a trigger from any table.
-   It must not commit or roll back the current transaction or change the isolation level.
-   Before triggers cannot have <span class="CodeFont">INSERT</span>, <span class="CodeFont">UPDATE</span>, <span class="CodeFont">SELECT</span>, or <span class="CodeFont">DELETE</span> statements as their action.
-   Before triggers cannot call procedures that modify SQL data as their action.
-   The <span class="CodeFont">NEW</span> variable of a <span class="CodeFont">BEFORE</span> trigger cannot reference a generated column.

The statement can reference database objects other than the table upon which the trigger is declared. If any of these database objects is dropped, the trigger is invalidated. If the trigger cannot be successfully recompiled upon the next execution, the invocation throws an exception and the statement that caused it to fire will be rolled back.

<a href="" id="ReferencingClause"></a>The Referencing Clause

Many triggered-SQL-statements need to refer to data that is currently being changed by the database event that caused them to fire. The triggered-SQL-statement might need to refer to the old (pre-change or <span class="ItalicFont">before</span>) values or to the new (post-change or <span class="ItalicFont">after</span>) values. You can refer to the data that is currently being changed by the database event that caused the trigger to fire.

Note that the referencing clause can designate only one new correlation or identifier and only one old correlation or identifier.

Transition Variables in Row Triggers

Use the transition variables <span class="CodeFont">OLD</span> and <span class="CodeFont">NEW</span> with row triggers to refer to a single row before (<span class="CodeFont">OLD</span>) or after (<span class="CodeFont">NEW</span>) modification. For example:

``` Example
REFERENCING OLD AS DELETEDROW;
```

You can then refer to this correlation name in the triggered-SQL-statement:

``` Example
splice> DELETE FROM HotelAvailability WHERE hotel_id = DELETEDROW.hotel_id;
```

The <span class="CodeFont">OLD</span> and <span class="CodeFont">NEW</span> transition variables map to a <span class="ItalicFont">java.sql.ResultSet</span> with a single row.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">INSERT</span> row triggers cannot reference an <span class="CodeFont">OLD</span> row.
<span class="CodeFont">DELETE</span> row triggers cannot reference a <span class="CodeFont">NEW</span> row.

Trigger Recursion

The maximum trigger recursion depth is 16.

Examples

This section presents examples of creating triggers:

A statement trigger:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE
   ON TARGET_TABLE
   FOR EACH STATEMENT
       INSERT INTO AUDIT_TABLE VALUES (CURRENT_TIMESTAMP, 'TARGET_TABLE was updated');
0 rows inserted/updated/deleted
```

A statement trigger calling a custom stored procedure:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE
   ON TARGET_TABLE
   FOR EACH STATEMENT
      CALL my_custom_stored_procedure('arg1', 'arg2');
0 rows inserted/updated/deleted
```

A simple row trigger:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE
   ON TARGET_TABLE
   FOR EACH ROW
      INSERT INTO AUDIT_TABLE VALUES (CURRENT_TIMESTAMP, 'TARGET_TABLE row was updated');
0 rows inserted/updated/deleted
```

A row trigger defined on a subset of columns:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE OF col1, col2
   ON TARGET_TABLE
   FOR EACH ROW
      INSERT INTO AUDIT_TABLE VALUES (CURRENT_TIMESTAMP, 'TARGET_TABLE col1 or col2 of row was updated');
0 rows inserted/updated/deleted
```

``` Example
splice> CREATE TRIGGER UpdateSingles
   AFTER UPDATE OF Hits, Doubles, Triples, Homeruns
   ON Batting
   FOR EACH ROW
   UPDATE Batting Set Singles=(Hits-(Doubles+Triples+Homeruns));
0 rows insert/updated/deleted
```

A row trigger defined on a subset of columns, referencing new and old values:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE OF col1, col2
   ON T
   REFERENCING OLD AS OLD_ROW NEW AS NEW_ROW
   FOR EACH ROW
      INSERT INTO AUDIT_TABLE VALUES (CURRENT_TIMESTAMP, 'TARGET_TABLE row was updated', OLD_ROW.col1, NEW_ROW.col1);
0 rows insert/updated/deleted
```

A row trigger defined on a subset of columns, referencing new and old values, calling custom stored procedure:

``` Example
splice> CREATE TRIGGER triggerName
   AFTER UPDATE OF col1, col2
   ON T
   REFERENCING OLD AS OLD_ROW NEW AS NEW_ROW
   FOR EACH ROW
      CALL my_custom_stored_procedure('arg1', 'arg2', OLD_ROW.col1, NEW_ROW.col1);
0 rows insert/updated/deleted
```

See Also

-   [Database Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) in the <span class="ItalicFont">Developer's Guide</span>
-   <span class="CodeFont">[DROP TRIGGER](DropTrigger.html)</span> statement
-   <span class="CodeFont">[WHERE](../Clauses/Where.html)</span> clause

 


