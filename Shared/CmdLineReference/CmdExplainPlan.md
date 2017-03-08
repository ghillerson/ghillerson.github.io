[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdExplainPlan.html)

[]()Explain Plan Command
========================

The <span class="AppCommand">explain</span> command displays the execution plan for a statement without actually executing the statement; it parses and optimizes the SQL, then presents its execution plan.

You can use this to tune a query for improved performance.

Syntax

``` FcnSyntax
explain Statement ]
```

<span class="ItalicFont">Statement</span>

An SQL statement.

Usage

SQL Data Definition Language (DDL) statement have no known cost, and thus do not require optimization. Because of this, the <span class="CodeFont">explain</span> command does not work with DDL statements; attempting to <span class="CodeFont">explain</span> a DDL statement such as <span class="CodeFont">CREATE TABLE</span> will generate a syntax error.

For more information about using the explain command, including a number of annotated examples, see the [Explain Plan](../Developers/TuningAndDebugging/ExplainPlan.html) topic in the <span class="ItalicFont">Performance Tuning</span> section of our <span class="ItalicFont">Administrator's Guide</span>.

Examples

``` AppCommand
splice> explain select * from t t1 where t1.i < (select max(i) from t t1);
```

The [Explain Plan](../Developers/TuningAndDebugging/ExplainPlan.html) topic in the <span class="ItalicFont">Performance Tuning</span> section of our <span class="ItalicFont">Administrator's Guide</span> contains a number of examples that are described in detail.

 


