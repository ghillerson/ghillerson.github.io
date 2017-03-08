[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/UpdateSystemProcedure.html)

<a href="" id="BuiltInSysProcs.UpdateSystemProcedure"></a>[]()SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE
==========================================================================================================

The SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE system procedure updates the stored declaration of a specific system procedure in the data dictionary. Call this procedure after adding a new system procedure or modifying an existing system procedure.

About System Procedures

Splice Machine uses prepared statements known as <span class="ItalicFont">system procedures</span> to access data in the system tables. Each system procedure has two parts:

-   An <span class="ItalicFont">implementation</span>, which is compiled Java byte code that is stored in the Splice jar and is included in the CLASSPATH of the Splice server.
-   A <span class="ItalicFont">declaration</span> (or <span class="ItalicFont">signature</span>), which is a <span class="CodeFont">CREATE PROCEDURE</span> statement that is stored in the Splice jar file and is synchronized with the data dictionary (in the <span class="CodeFont">SYSALIASES</span> table).

The <span class="CodeFont">SYSALIASES</span> table is synchronized with a database when the database is first created. Thereafter, when you make changes to the system procedures, you need to call a function to keep the <span class="CodeFont">SYSALIASES</span> table synchronized with the procedures in the Splice jar file.

If you've modified, deleted, or added a system procedure, call this function, <span class="CodeFont">SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE</span>, which drops the procedure from the data dictionary, and updates the dictionary with the new version in the Splice jar file.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_UPDATE_SYSTEM_PROCEDURE(schemaName, procName)
```

schemaName

A string specifying the name of the schema that needs to be updated in the data dictionary.

procName

A string specifying the name of the system procedure whose declaration needs to be updated in the data dictionary.

Results

This procedure does not return a result.

Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_UPDATE_SYSTEM_PROCEDURE('SYSCS_UTIL', 'IMPORT_DATA');
Statement executed.
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL\_SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES</span>](UpdateAllSystemProcedures.html)

 


