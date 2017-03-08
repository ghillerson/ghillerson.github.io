[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdShowFunctions.html)

[]()Show Functions
==================

The <span class="AppCommand">show functions</span> command displays all of the functions in the database, or the names of the functions in the specified schema.

Syntax

``` FcnSyntax
SHOW FUNCTIONS [ IN schemaName ]
```

schemaName

If you supply a schema name, only the functions in that schema are displayed; otherwise, all functions in the database are displayed.

Results

The <span class="AppCommand">show functions</span> command results contains the following columns:

| Column Name      | Description                                        |
|------------------|----------------------------------------------------|
| FUNCTION\_SCHEMA | The name of the function's schema                  |
| FUNCTION\_NAME   | The name of the function                           |
| REMARKS          | Any remarks that have been stored for the function |

Examples

``` AppCommand
splice> CREATE FUNCTION TO_DEGREES ( RADIANS DOUBLE )
> RETURNS DOUBLE
> PARAMETER STYLE JAVA
> NO SQL LANGUAGE JAVA
> EXTERNAL NAME 'java.lang.Math.toDegrees';
0 rows inserted/updated/deleted
splice> show functions in splice;
FUNCTION_SCHEM|FUNCTION_NAME               |REMARKS
-------------------------------------------------------------------------
SPLICE        |TO_DEGREES                  |java.lang.Math.toDegrees           

1 row selected
```

 


