[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/ForeignKeys.html)

Foreign Keys and Referential Integrity
======================================

This topic describes the Splice Machine implementation of <span class="ItalicFont">foreign keys</span> and how our implementation ensures referential integrity.

See our <span class="ItalicFont">SQL Reference Manual</span> for full reference information about defining foreign keys using [constraint clauses](../../SQLReference/Clauses/Constraint.html) when [creating](../../SQLReference/Statements/CreateTable.html)a database table.

About Foreign Keys
------------------

A foreign key is a column or group of columns in a relational database table that provides a link between data in two tables. A foreign key acts as a cross-reference between tables in that it references the primary key or unique key columns of another table, and thus establishes a link between them.

The purpose of a foreign key is to identify a particular row of the referenced table; as such, the foreign key must be equal to the key in some row of the primary table, or else be <span class="CodeFont">null</span>. This rule is called a <span class="ItalicFont">referential integrity constraint between the two tables</span>, and is usually abbreviated as just <span class="ItalicFont">referential integrity</span>.

### Maintaining Referential Integrity

To maintain referential integrity, Splice Machine ensures that database operations do not violate foreign key constraints, including not allowing any operations that will cause a foreign key to not correspond to a row in the referenced table. This can happen when a row is inserted, updated, or deleted in either table.

For example, suppose you have:

-   A table named <span class="CodeFont">Players</span> with primary key <span class="CodeFont">player\_id</span>. This table is called the <span class="ItalicFont">parent table</span> or <span class="ItalicFont">referenced table</span>.
-   A second table named <span class="CodeFont">PlayerStats</span> has a foreign key, which is also a column named <span class="CodeFont">player\_id</span>. This table is called the <span class="ItalicFont">child table</span> or <span class="ItalicFont">referencing table</span>.

The <span class="CodeFont">player\_id</span> column in the <span class="ItalicFont">referencing</span> table is the foreign key that references the primary key <span class="CodeFont">player\_id</span> in the <span class="ItalicFont">referenced</span> table.

When you insert a new record into the referencing <span class="CodeFont">PlayerStats</span> table, the insertion must satisfy the foreign key constraint, which means that it must include a <span class="CodeFont">player\_id</span> value that is present in the referenced <span class="CodeFont">Players</span> table. If this is not so, the insert operation fails in order to maintain the table's referential integrity.

### About Foreign Key Constraints

You can define a foreign key constraint on a table when you create the table with the <span class="CodeFont">[CREATE TABLE](../../SQLReference/Statements/CreateTable.html)</span> statement. Foreign key constraints are always immediate: a violation of a constraint immediately throws an exception.

Here's an example of defining a foreign key, in which we use the <span class="CodeFont">REFERENCES</span> clause of a column definition in a <span class="CodeFont">CREATE TABLE</span> statement:

``` Example
CREATE TABLE t1 (c1 NUMERIC PRIMARY KEY);

CREATE TABLE t2 (
   c1 NUMERIC PRIMARY KEY,
   c2 NUMERIC REFERENCES t1(c1) );
```

And here's an example that uses the <span class="CodeFont">[CONSTRAINT](../../SQLReference/Clauses/Constraint.html)</span> clause to name the foreign key constraint:

``` Example
CREATE TABLE t3 (
   c1 NUMERIC, 
   c2 NUMERIC,
   CONSTRAINT t1_fkey FOREIGN KEY (c1) REFERENCES t1);
```

You can also define a foreign key on a combination of columns:

``` Example
CREATE TABLE dept_20
   (employee_id INT, hire_date DATE,
   CONSTRAINT fkey_empid_hiredate
   FOREIGN KEY (employee_id, hire_date)
   REFERENCES dept_21(employee_id, start_date));
```

See Also
--------

-   <span class="CodeFont">[ALTER TABLE](../../SQLReference/Statements/AlterTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CONSTRAINT](../../SQLReference/Clauses/Constraint.html)</span> clause in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[CREATE TABLE](../../SQLReference/Statements/CreateTable.html)</span> statement in the <span class="ItalicFont">SQL Reference Manual</span>
-   [Using Database Triggers](DatabaseTriggers.html)

 

 


