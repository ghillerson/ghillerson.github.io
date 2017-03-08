[Open topic with navigation](../index.html#OnPremise/CurrentReleaseNotes.html)

Release Notes for Splice Machine Version <span class="BasicVariablesSpliceReleaseVersion">2.5</span>
====================================================================================================

This topic lists any notes applicable to this release that may be of interest to developers. These can include previously unstated limitations or workarounds for problems that will be fixed in a future release.

For information about important new features added in this and previous releases, see the [Update Notes for Splice Machine Version 2.5](CurrentUpdateNotes.html).
The <span class="CodeFont">ReadMe</span> file included with the Splice Machine installers contains a list of specific bug fixes in this release.

These are the notes and workarounds for known issues in our current release:

-   <a href="#Changes" class="WithinBook">Changes to Bulk Import</a>
-   [Temporary Tables and Backups](#Temporar)
-   [Natural Self Joins Not Supported](#Natural)
-   [Columnar screen output gets truncated](#Columnar)
-   [TimeStamp date value limitations](#Timestam)
-   [<span class="CodeFont">ToDate</span> function problem with <span class="CodeFont">DD</span> designator](#ToDate())
-   [Dropping Foreign Keys](#Dropping)
-   [Compaction Queue Issue](#Compacti)
-   [Alter Table Issues](#AlterTbl)
-   [<span class="CodeFont">Lead</span> and <span class="CodeFont">Lag</span> default value parameter](#LeadLag)
-   [<span class="CodeFont">CREATE TABLE AS</span> with <span class="CodeFont">RIGHT OUTER JOIN</span>](#CREATET)
-   [Import Performance Issues With Many Foreign Key References](#TooManyForeignKeyRefs)

[]()Changes to Bulk Import
--------------------------

We've updated our data import technology for improved performance and better error handling. We <span class="BoldFont">strongly advise</span> that you visit the [Importing Data](../Shared/Developers/ImportingData.html) topic in this <span class="ItalicFont">Administrator's Guide</span> to review the changes. The same changes are noted in the reference pages for the two bulk import built-in system procedures:

The number of parameters and the meaning of certain parameters has changed in these built-in system procedures:

-   [SYSCS\_UTIL.IMPORT\_DATA](../Shared/SQLReference/BuiltInSysProcs/ImportData.html)
-   [SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE](../Shared/SQLReference/BuiltInSysProcs/UpsertDataFromFile.html)

We <span class="BoldFont">strongly advise</span> that you visit the [Importing Data](../Shared/Developers/ImportingData.html) topic in this <span class="ItalicFont">Administrator's Guide</span> to review the changes.

A few specifics that you should be aware of if you're upgrading from a previous version of Splice Machine:

-   The parameter previously named <span class="CodeFont">failedBadRecordCount</span> is now named <span class="CodeFont">badRecordsAllowed</span>. The meaning of this parameter value is now different:
    -   <span class="BoldFont">Supply a value of <span class="CodeBoldFont">-1</span> for <span class="CodeBoldFont">badRecordsAllowed</span> to continue importing records no matter how many bad records are encountered.</span> (In previous versions of Splice Machine, a value of <span class="CodeFont">0</span> was used for this purpose).
    -   <span class="BoldFont">Supply a value of <span class="CodeBoldFont">0</span> for <span class="CodeBoldFont">badRecordsAllowed</span> to halt the import process as soon as a single bad record is encountered.</span>
-   How bulk imports handle generated column values and white space is now spelled out in detail in the documentation
-   We strongly recommend that you explicitly specify <span class="CodeFont">DATE</span> and <span class="CodeFont">TIMESTAMP</span> column formats when importing data; previous versions of Splice Machine could handle more formats by default.

[]()Natural Self Joins Not Supported
------------------------------------

Splice Machine does not currently support <span class="CodeFont">NATURAL SELF JOIN</span> operations.

[]()Temporary Tables and Backups
--------------------------------

There's a subtle issue with performing a backup when you're using a temporary table in your session: although the temporary table is (correctly) not backed up, the temporary table's entry in the system tables will be backed up. When the backup is restored, the table entries will be restored, but the temporary table will be missing.

There's a simple workaround:

1.  Exit your current session, which will automatically delete the temporary table and its system table entries.
2.  Start a new session (reconnect to your database).
3.  Start your backup job.

[]()Columnar screen output gets truncated
-----------------------------------------

When using <span class="CodeFont">Explain Plan</span> and other commands that generate lengthy output lines, you may see some output columns truncated on the screen.

<span class="autonumber"><span class="noteAutoNum">WORKAROUND:  </span></span>Use the <span class="AppCommand">maximumdisplaywidth=0</span>command to force all column contents to be displayed.

[]()TimeStamp date value limitations
------------------------------------

Dates in <span class="CodeFont">[TIMESTAMP Data Type](../Shared/SQLReference/DataTypes/TimeStamp.html)</span> values only work correctly when limited to this range of date values:

    1678-01-01 to 2261-12-31

[]()<span class="CodeFont">ToDate</span> function problem with DD designator
----------------------------------------------------------------------------

The <span class="CodeFont">[TO\_DATE](../Shared/SQLReference/BuiltInFcns/ToDate.html)</span> function currently returns the wrong date if you specify <span class="CodeFont">DD</span> for the day field; however, specifying <span class="CodeFont">dd</span> instead works properly.

<span class="autonumber"><span class="noteAutoNum">WORKAROUND:  </span></span>Use <span class="CodeFont">dd</span> instead of <span class="CodeFont">DD</span>.

[]()Dropping Foreign Keys
-------------------------

The <span class="CodeFont">DROP FOREIGN KEY</span> clause of the <span class="CodeFont">[ALTER TABLE](../Shared/SQLReference/Statements/AlterTable.html)</span> statement is currently unavailable in Splice Machine.

<span class="autonumber"><span class="noteAutoNum">WORKAROUND:  </span></span>Re-create the table without the foreign key constraint.

[]()Compaction Queue Issue
--------------------------

We have seen a problem in which the compaction queue grows quite large after importing large amounts of data, and are investigating a solution; for now, please use the following workaround.

<span class="autonumber"><span class="noteAutoNum">WORKAROUND:  </span></span>Run a full compaction on tables into which you have imported a large amount of data, using the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE](../Shared/SQLReference/BuiltInSysProcs/PerformMajorCompactionOnTable.html)</span> system procedure.

[]()Alter Table Issues
----------------------

Using <span class="CodeFont">ALTER TABLE</span> against <span class="CodeFont">PRIMARY KEY</span> columns does not currently work properly.

[]()Default Value for Lead and Lag Functions
--------------------------------------------

This release of Splice Machine features several new window functions, including <span class="CodeFont">[LEAD](../Shared/SQLReference/BuiltInFcns/Lead.html)</span> and <span class="CodeFont">[LAG](../Shared/SQLReference/BuiltInFcns/Lag.html)</span>. Currently, our implementations of <span class="CodeFont">[LEAD](../Shared/SQLReference/BuiltInFcns/Lead.html)</span> and <span class="CodeFont">[LAG](../Shared/SQLReference/BuiltInFcns/Lag.html)</span> do not support the default value parameter that you can specify in some other implementations. We expect to add this parameter in future releases.

[]()CREATE TABLE AS with RIGHT OUTER JOIN
-----------------------------------------

There is a known problem using the <span class="CodeFont">CREATE TABLE AS</span> form of the <span class="CodeFont">[CREATE TABLE](../Shared/SQLReference/Statements/CreateTable.html)</span> statement .when the data to be inserted into the new table results from a <span class="CodeFont">[RIGHT OUTER JOIN](../Shared/SQLReference/JoinOps/RightOuterJoin.html)</span> operation. For example, the following statement currently produces a table with all <span class="CodeFont">NULL</span> values:

``` Example
CREATE TABLE t3 AS
   SELECT t1.a,t1.b,t2.c,t2.d
   FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c
   WITH DATA;
```

There's a simple workaround for now: create the table without inserting the data, and then insert the data; for example:

``` Example
CREATE TABLE t3 AS
   SELECT t1.a,t1.b,t2.c,t2.d
   FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c
   WITH NO DATA;

INSERT INTO t3
   SELECT t1.a,t1.b,t2.c,t2.d 
   FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c;
```

[]()Import Performance Issues With Many Foreign Key References
--------------------------------------------------------------

The presence of many foreign key references on a table will slow down imports of data into that table.

 


