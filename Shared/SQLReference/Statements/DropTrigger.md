[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/DropTrigger.html)

<a href="" id="Statements.DropTrigger"></a>[]()DROP TRIGGER
===========================================================

The <span class="CodeFont">DROP TRIGGER</span> statement removes the specified trigger.

Syntax

``` FcnSyntax
DROP TRIGGER TriggerName
```

TriggerName

The name of the trigger that you want to drop from your database.

Example

``` Example
splice> DROP TRIGGER UpdateSingles;
0 rows inserted/updated/deleted
```

Statement dependency system

When a table is dropped, all triggers on that table are automatically dropped; this means that do not have to drop a table's triggers before dropping the table.

See Also

-   [Database Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) in the <span class="ItalicFont">Developer's Guide</span>
-   <span class="CodeFont">[CREATE TRIGGER](CreateTrigger.html)</span> statement

 


