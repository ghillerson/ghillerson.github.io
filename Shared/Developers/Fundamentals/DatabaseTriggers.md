[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/DatabaseTriggers.html)

Using Database Triggers
=======================

This topic describes database triggers and how you can use them with Splice Machine.

About Database Triggers
-----------------------

A database trigger is procedural code that is automatically executed in response to certain events on a particular table or view in a database. Triggers are mostly used for maintaining the integrity of the information on the database; they are most commonly used to:

-   automatically generate derived column values
-   enforce complex security authorizations
-   enforce referential integrity across nodes in a distributed database
-   enforce complex business rules
-   provide transparent event logging
-   provide sophisticated auditing
-   gather statistics on table access

### Components of a Trigger

Each trigger has two required components:

| Component                       | Description                                                                                                                                                                            |
|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Triggering event (or statement) | The SQL statement that causes a trigger to be fired. This can be one of the following types of statement:                                                                              
                                                                                                                                                                                                                           
                                   -   INSERT                                                                                                                                                                              
                                   -   UPDATE                                                                                                                                                                              
                                   -   DELETE                                                                                                                                                                              |
| Trigger action                  | The procedure that contains the SQL statements to be executed when a triggering statement is issued and any trigger restrictions evaluate to <span class="CodeFont">TRUE</span>.       
                                                                                                                                                                                                                           
                                   A trigger action is one of the following:                                                                                                                                               
                                                                                                                                                                                                                           
                                   -   arbitrary SQL                                                                                                                                                                       
                                   -   a call to a [built-in stored procedure](../../SQLReference/BuiltInSysProcs/Intro.BuiltInSysProcs.html) or [user-defined stored procedure](../FcnsAndProcs/Intro.FcnsAndProcs.html)  |

### When a Trigger Fires

You can define both statement and row triggers as either <span class="ItalicFont">before triggers</span> or <span class="ItalicFont">after triggers</span>:

| Trigger Type    | Description                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------|
| Before Triggers | A before trigger fires before the statement's changes are applied and before any constraints have been applied.               |
| After Triggers  | An after trigger fires after all constraints have been satisfied and after the changes have been applied to the target table. |

### How Often a Trigger Fires

You can define triggers as either <span class="ItalicFont">statement triggers</span> or <span class="ItalicFont">row triggers</span>, which defines how often a trigger will fire for a triggering event.

| Trigger Type       | Description                                                                                                                                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Statement Triggers | A statement trigger fires once per triggering event, regardless of how many rows (including zero rows) are modified by the event.                                                                                                     |
| Row Triggers       | A row trigger fires once for each row that is affected by the triggering event; for example, each row modified by an <span class="CodeFont">UPDATE</span> statement. If no rows are affected by the event, the trigger does not fire. |

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Triggers are statement triggers by default. You specify a row trigger in the <span class="CodeFont">FOR EACH</span> clause of the <span class="CodeFont">[CREATE TRIGGER](../../SQLReference/Statements/CreateTrigger.html)</span> statement.

Examples
--------

This section presents examples of using database triggers.

### Example 1: Row Level AFTER Trigger

This example shows a row level trigger that is called after a row is updated in the <span class="CodeFont">employees</span> table. The action of this trigger is to insert one record into the audit trail table (<span class="CodeFont">employees\_log</span>) for each record that gets updated in the <span class="CodeFont">employees</span> table.

``` Example
CREATE TRIGGER log_salary_increase
AFTER UPDATE ON employees FOR EACH ROW
   INSERT INTO employees_log
     (emp_id, log_date, new_salary, action)
   VALUES
     (:new.empno, CURRENT_DATE, :new.salary, 'NEW SALARY');
```

If you then issue following statement to update salaries of all employees in the PD department:

``` Example
UPDATE employees SET salary = salary + 1000.0 WHERE department = 'PD';
```

Then the trigger will fire once (and one audit record will be inserted) for each employee in the department named <span class="CodeFont">PD</span>.

### Example 2: Statement Level After Trigger

This example shows a statement level trigger that is called after the <span class="CodeFont">employees</span> table is updated. The action of this trigger is to insert exactly one record into the change history table (<span class="CodeFont">reviews\_history</span>) whenever the <span class="CodeFont">employee\_reviews</span> table is updated.

This example shows a row level trigger that is called after a row is updated in the <span class="CodeFont">employees</span> table. The action of this trigger is to insert one record into the audit trail table (<span class="CodeFont">employees\_log</span>) for each record that gets updated in the <span class="CodeFont">employees</span> table.

``` Example
CREATE TRIGGER log_salary_increase
AFTER UPDATE ON employees referencing NEW as NEW FOR EACH ROW
INSERT INTO employees_log
(emp_id, log_date, new_salary, action)
VALUES
(NEW.empno, CURRENT_DATE, NEW.salary, 'NEW SALARY');
```

If you then issue the same Update statement as used in the previous example:

``` Example
UPDATE employees SET salary = salary + 1000.0 WHERE department = 'PD';
```

Then the trigger will fire once and exactly one record will be inserted into the <span class="CodeFont">employees\_log</span> table, no matter how many records are updated by the statement.

### Example 3: Statement Level Before Trigger

This example shows a row level trigger that is called before a row is inserted into the <span class="CodeFont">employees</span> table.

``` Example
CREATE TRIGGER empUpdateTrig
BEFORE UPDATE ON employees
   FOR EACH STATEMENT SELECT ID FROM myTbl;
```

See Also
--------

-   <span class="CodeFont">[CREATE TRIGGER](../../SQLReference/Statements/CreateTrigger.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[DROP TRIGGER](../../SQLReference/Statements/DropTrigger.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   [Foreign keys](ForeignKeys.html)
-   <span class="CodeFont">[UPDATE](../../SQLReference/Statements/UpdateTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[WHERE](../../SQLReference/Clauses/Where.html)</span> clause in the <span class="ItalicFont">SQL Reference Manual</span>

 


