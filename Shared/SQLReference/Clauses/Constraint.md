[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Constraint.html)

<a href="" id="Clauses.Constraint"></a>[]()CONSTRAINT
=====================================================

A <span class="CodeFont">CONSTRAINT</span> clause is a rule to which data must conform, and is an optional part of [<span class="CodeFont">CREATE TABLE</span>](../Statements/CreateTable.html) and [<span class="CodeFont">ALTER TABLE</span>](../Statements/AlterTable.html) statements. Constraints can optionally be named.

There are two types of constraints:

column-level constraints

A column-level constraint refers to a single column in a table (the column that it follows syntactically) in the table. Column constraints, other than <span class="CodeFont">CHECK </span>constraints, do not specify a column name.

table-level constraints

A table-level constraints refers to one or more columns in a table by specifying the names of those columns. Table-level <span class="CodeFont">CHECK</span> constraints can refer to 0 or more columns in the table.

Column constraints and table constraints have the same function; the difference is in where you specify them.

-   Table constraints allow you to specify more than one column in a <span class="CodeFont">PRIMARY KEY </span> or <span class="CodeFont">CHECK </span><span>, <span class="CodeFont">UNIQUE</span> or <span class="CodeFont">FOREIGN KEY</span></span> constraint definition.
-   Column-level constraints (except for check constraints) refer to only one column.

<a href="" id="ColumnConstraint"></a>Column Constraints

``` FcnSyntax
{
NOT NULL |
[ [CONSTRAINT constraint-Name]
{PRIMARY KEY}
}
```

``` FcnSyntax
{
NOT NULL |
[ [CONSTRAINT constraint-Name]
{
CHECK (searchCondition) |
{
PRIMARY KEY |
UNIQUE |
REFERENCES clause
} 
}
}
```

NOT NULL

Specifies that this column cannot hold <span class="CodeFont">NULL</span> values (constraints of this type are not nameable).

PRIMARY KEY

Specifies the column that uniquely identifies a row in the table. The identified columns must be defined as <span class="CodeFont">NOT NULL</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>At this time, you <span class="BoldFont">cannot</span> add a primary key using <span class="CodeFont">ALTER TABLE</span>. This is being addressed in our next release.

UNIQUE

Specifies that values in the column must be unique.

FOREIGN KEY

Specifies that the values in the column must correspond to values in a referenced primary key or unique key column or that they are NULL.

CHECK

Specifies rules for values in the column.

<a href="" id="TableConstraint"></a>Table Constraints

``` FcnSyntax
[CONSTRAINT constraint-Name]
{
   PRIMARY KEY ( Simple-column-Name
   [ , Simple-column-Name ]* )
}
```

``` FcnSyntax
[CONSTRAINT constraint-Name]
{
   CHECK (searchCondition) |
   {
   PRIMARY KEY ( Simple-column-Name
   [ , Simple-column-Name ]* ) |
   UNIQUE ( Simple-column-Name
   [ , Simple-column-Name ]* ) |
   FOREIGN KEY (
   Simple-column-Name
   [ , Simple-column-Name ]* )
   REFERENCES clause
   }
}
```

PRIMARY KEY

Specifies the column or columns that uniquely identify a row in the table. <span class="CodeFont">NULL</span> values are not allowed.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>At this time, you <span class="BoldFont">cannot</span> add a primary key using <span class="CodeFont">ALTER TABLE</span>. This is being addressed in our next release.

UNIQUE

Specifies that values in the columns must be unique.

FOREIGN KEY

Specifies that the values in the columns must correspond to values in referenced primary key or unique columns or that they are <span class="CodeFont">NULL</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If the foreign key consists of multiple columns, and <span class="ItalicFont">any</span> column is <span class="CodeFont">NULL</span>, the whole key is considered <span class="CodeFont">NULL</span>. The insert is permitted no matter what is on the non-null columns.

CHECK

Specifies a wide range of rules for values in the table.

Primary Key Constraints

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>At this time, you <span class="BoldFont">cannot</span> alter primary keys using <span class="CodeFont">ALTER TABLE</span>. This is being addressed in our next release.

Primary keys are constrained as follows:

-   A primary key defines the set of columns that uniquely identifies rows in a table.
-   When you create a primary key constraint, none of the columns included in the primary key can have <span class="CodeFont">NULL</span> constraints; that is, they must not permit <span class="CodeFont">NULL</span> values.
-   A table can have at most one <span class="CodeFont">PRIMARY KEY</span> constraint.

Unique constraints

A <span class="CodeFont">UNIQUE</span> constraint defines a set of columns that uniquely identify rows in a table only if all the key values are not <span class="CodeFont">NULL</span>. If one or more key parts are <span class="CodeFont">NULL</span>, duplicate keys are allowed.

For example, if there is a <span class="CodeFont">UNIQUE</span> constraint on col1 and col2 of a table, the combination of the values held by col1 and col2 will be unique as long as these values are not <span class="CodeFont">NULL</span>. If one of col1 and col2 holds a <span class="CodeFont">NULL</span> value, there can be another identical row in the table.

A table can have multiple <span class="CodeFont">UNIQUE</span> constraints.

Foreign key constraints

Foreign keys providea way to enforce the referential integrity of a database. A foreign key is a column or group of columns within a table that references a key in some other table (or sometimes the same table). The foreign key must always include the columns of which the types exactly match those in the referenced primary key or unique constraint.

For a table-level foreign key constraint in which you specify the columns in the table that make up the constraint, you cannot use the same column more than once.

If there is a column list in the <span class="ItalicFont">ReferencesSpecification </span>(a list of columns in the referenced table), it must correspond either to a unique constraint or to a primary key constraint in the referenced table. The <span class="ItalicFont">ReferencesSpecification</span> can omit the column list for the referenced table if that table has a declared primary key.

If there is no column list in the <span class="ItalicFont">ReferencesSpecification </span>and the referenced table has no primary key, a statement exception is thrown. (This means that if the referenced table has only unique keys, you must include a column list in the <span class="ItalicFont">ReferencesSpecification.</span>)

A foreign key constraint is satisfied if there is a matching value in the referenced unique or primary key column. If the foreign key consists of multiple columns, the foreign key value is considered <span class="CodeFont">NULL</span> if any of its columns contains a <span class="CodeFont">NULL</span>.

It is possible for a foreign key consisting of multiple columns to allow one of the columns to contain a value for which there is no matching value in the referenced columns, per the ANSI SQL standard. To avoid this situation, create <span class="CodeFont">NOT NULL</span> constraints on all of the foreign key's columns.

Foreign key constraints and DML

When you insert into or update a table with an enabled foreign key constraint, Splice Machine checks that the row does not violate the foreign key constraint by looking up the corresponding referenced key in the referenced table. If the constraint is not satisfied, Splice Machine rejects the insert or update with a statement exception.

When you update or delete a row in a table with a referenced key (a primary or unique constraint referenced by a foreign key), Splice Machine checks every foreign key constraint that references the key to make sure that the removal or modification of the row does not cause a constraint violation.

If removal or modification of the row would cause a constraint violation, the update or delete is not permitted and Splice Machine throws a statement exception.

Splice Machine performs constraint checks at the time the statement is executed, not when the transaction commits.

<span class="CodeFont">PRIMARY KEY</span> constraints generate unique indexes. <span class="CodeFont">FOREIGN KEY</span> constraints generate non-unique indexes.

<span class="CodeFont">UNIQUE</span> constraints generate unique indexes if all the columns are non-nullable, and they generate non-unique indexes if one or more columns are nullable.

Therefore, if a column or set of columns has a <span class="CodeFont">UNIQUE</span>, <span class="CodeFont">PRIMARY KEY</span>, or <span class="CodeFont">FOREIGN KEY</span> constraint on it, you do not need to create an index on those columns for performance. Splice Machine has already created it for you.

Check constraints

You can use check constraints to limit which values are accepted by one or more columns in a table. You specify the constraint with a Boolean expression; if the expression evaluates to <span class="CodeFont">true</span>, the value is allowed; if the expression evaluates to <span class="CodeFont">false</span>, the constraint prevents the value from being entered into the database.The search condition is applied to each row that is modified on an <span class="CodeFont">INSERT</span> or <span class="CodeFont">UPDATE</span> at the time of the row modification. When a constraint is violated, the entire statement is aborted. You can apply check constraints at the column level or table level.

For example, you could specify that values in the salary column for the players on your team must be between $250,000 and $30,000,000 with this expression:

``` Example
salary >= 250000 AND salary <= 30000000.
```

Any attempt to insert or update a record with a salary value out of that range would fail.

<a href="" id="SearchCondition"></a>Search Condition

A <span class="ItalicFont">searchCondition</span> is any [Boolean expression](../Expressions/BooleanExpressions.html) that meets the requirements specified below. If a <span class="ItalicFont">constraint-Name</span> is not specified, Splice Machine generates a unique constraint name (for either column or table constraints).

Requirements for search condition

If a check constraint is specified as part of a column-definition, a column reference can only be made to the same column. Check constraints specified as part of a table definition can have column references identifying columns previously defined in the <span class="CodeFont">[CREATE TABLE](../Statements/CreateTable.html)</span> statement.

The search condition must always return the same value if applied to the same values. Thus, it cannot contain any of the following:

-   Dynamic parameters
-   Date/Time Functions (<span class="CodeFont">[CURRENT\_DATE](../BuiltInFcns/CurrentDate.html)</span>, <span class="CodeFont">[CURRENT\_TIME](../BuiltInFcns/CurrentTime.html)</span>, <span class="CodeFont">[CURRENT\_TIMESTAMP](../BuiltInFcns/CurrentTimestamp.html)</span>)
-   Subqueries
-   User Functions (such as <span class="CodeFont">[USER](../BuiltInFcns/User.html)</span>, <span class="CodeFont">[SESSION\_USER](../BuiltInFcns/SessionUser.html)</span>, <span class="CodeFont">[CURRENT\_USER](../BuiltInFcns/CurrentUser.html)</span>)

Examples

``` Example
   -- column-level primary key constraint named OUT_TRAY_PK:
CREATE TABLE SAMP.OUT_TRAY
(
SENT TIMESTAMP,
DESTINATION CHAR(8),
SUBJECT CHAR(64) NOT NULL CONSTRAINT
OUT_TRAY_PK PRIMARY KEY,
NOTE_TEXT VARCHAR(3000) 
);

-- the table-level primary key definition allows you to
-- include two columns in the primary key definition:
CREATE TABLE SAMP.SCHED 
(
CLASS_CODE CHAR(7) NOT NULL, 
DAY SMALLINT NOT NULL, 
STARTING TIME, 
ENDING TIME,
PRIMARY KEY (CLASS_CODE, DAY)
);
-- Use a column-level constraint for an arithmetic check
-- Use a table-level constraint
-- to make sure that a employee's taxes does not 
-- exceed the bonus
CREATE TABLE SAMP.EMP   
(
EMPNO CHAR(6) NOT NULL CONSTRAINT EMP_PK PRIMARY KEY,
FIRSTNME CHAR(12) NOT NULL,
MIDINIT vARCHAR(12) NOT NULL,
LASTNAME VARCHAR(15) NOT NULL,
SALARY DECIMAL(9,2) CONSTRAINT SAL_CK CHECK (SALARY >= 10000),
BONUS DECIMAL(9,2), 
TAX DECIMAL(9,2),
CONSTRAINT BONUS_CK CHECK (BONUS > TAX)
);

-- use a check constraint to allow only appropriate
-- abbreviations for the meals
CREATE TABLE FLIGHTS
(
FLIGHT_ID CHAR(6) NOT NULL ,
SEGMENT_NUMBER INTEGER NOT NULL ,
ORIG_AIRPORT CHAR(3),
DEPART_TIME TIME,
DEST_AIRPORT CHAR(3),
ARRIVE_TIME TIME,
MEAL CHAR(1) CONSTRAINT MEAL_CONSTRAINT 
CHECK (MEAL IN ('B', 'L', 'D', 'S')),
PRIMARY KEY (FLIGHT_ID, SEGMENT_NUMBER)
);
```

Statement dependency system

<span class="CodeFont">[INSERT](../Statements/Insert.html)</span> and <span class="CodeFont">[UPDATE](../Statements/UpdateTable.html)</span> statements depend on all constraints on the target table.

<span class="CodeFont">[DELETE](../Statements/Delete.html)</span> statements depend on unique<span>, primary key, and foreign key constraints</span>.

These statements are invalidated if a constraint is added to or dropped from the target table.

See Also

-   [<span class="CodeFont">ALTER TABLE</span>](../Statements/AlterTable.html) statement
-   [<span class="CodeFont">CREATE TABLE</span>](../Statements/CreateTable.html) statement
-   [<span class="CodeFont">INSERT</span>](../Statements/Insert.html) statement
-   [<span class="CodeFont">DELETE</span>](../Statements/Delete.html) statement
-   [Foreign Keys](../../Developers/Fundamentals/ForeignKeys.html) in the <span class="ItalicFont">Developer's Guide</span>.
-   [Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) in the <span class="ItalicFont">Developer's Guide</span>.
-   [<span class="CodeFont">UPDATE</span>](../Statements/UpdateTable.html) statement

 


