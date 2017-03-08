[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CallProcedure.html)

<a href="" id="Statements.CallProcedure"></a>[]()CALL (Procedure)
=================================================================

The <span class="CodeFont">CALL (PROCEDURE)</span> statement is used to call stored procedures.

When you call a stored procedure, the default schema and role are the same as were in effect when the procedure was created.

Syntax

``` FcnSyntax
CALL procedure-Name (
        [ expression [, expression]* ] 
)
```

procedure-Name

The name of the procedure that you are calling.

expression(s)

Arguments passed to the procedure.

Example

The following example depends on a fictionalized java class. For functional examples of using <span class="CodeFont">CREATE PROCEDURE</span>, please see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section in our <span class="ItalicFont">Developer's Guide</span>.

``` Example
splice> CREATE PROCEDURE SALES.TOTAL_REVENUE(IN S_MONTH INTEGER,
    IN S_YEAR INTEGER, OUT TOTAL DECIMAL(10,2))
    PARAMETER STYLE JAVA
      READS SQL DATA LANGUAGE JAVA EXTERNAL NAME 
       'com.example.sales.calculateRevenueByMonth';
splice> CALL SALES.TOTAL_REVENUE(?,?,?);
```

See Also

-   [<span class="CodeFont">CREATE PROCEDURE</span>](CreateProcedure.html) statement

 


