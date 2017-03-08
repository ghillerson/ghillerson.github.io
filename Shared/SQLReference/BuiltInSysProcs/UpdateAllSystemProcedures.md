[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/UpdateAllSystemProcedures.html)

<a href="" id="BuiltInSysProcs.UpdateAllSystemProcedures"></a>[]()SYSCS\_UTIL.SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES
====================================================================================================================

The SYSCS\_UTIL.SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES system procedure updates the signatures of all of the system procedures in a database.

<span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>You need to call this procedure when you update to a new version of Splice Machine that includes new or updates system procedure signatures.
The [Update Notes](../../../OnPremise/CurrentUpdateNotes.html) will note when a release includes such updates.

About System Procedures

Splice Machine uses prepared statements known as <span class="ItalicFont">system procedures</span> to access data in the system tables. Each system procedure has two parts:

-   An <span class="ItalicFont">implementation</span>, which is compiled Java byte code that is stored in the Splice jar and is included in the CLASSPATH of the Splice server.
-   A <span class="ItalicFont">declaration</span> (or <span class="ItalicFont">signature</span>), which is a CREATE PROCEDURE statement that is stored in the Splice jar file and is synchronized with the data dictionary (in the SYSALIASES table).

The <span class="CodeFont">SYSALIASES</span> table is synchronized with a database when the database is first created. Thereafter, when you make changes to the system procedures, you need to call a function to keep the <span class="CodeFont">SYSALIASES</span> table synchronized with the procedures in the Splice jar file.

If you've modified, deleted, or added a system procedure, call the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE](UpdateSystemProcedure.html)</span> function, which drops the procedure from the data dictionary, and updates the dictionary with the new version in the Splice jar file.

If you've made multiple modifications to the system procedures, you can call this function, <span class="CodeFont">SYSCS\_UTIL.SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES </span>, to update all of the stored declarations for a database in the data dictionary. This function drops all of the system procedures from the data dictionary and then recreates the system procedures stored in the dictionary from the definitions in the Splice jar file.

Results

This procedure does not return a result.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_UPDATE_ALL_SYSTEM_PROCEDURES(schemaName)
```

schemaName

A string specifying the name of the schema that needs to be updated in the data dictionary.

Example

``` Example
splice> call SYSCS_UTIL.SYSCS_UPDATE_ALL_SYSTEM_PROCEDURES('SYSCS_UTIL');
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL\_SYSCS\_UPDATE\_SYSTEM\_PROCEDURE</span>](#)

 


