[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdMaxDisplayWidth.html)

[]()MaximumDisplayWidth Command
===============================

The <span class="AppCommand">maximumdisplaywidth</span> command sets the largest display width, in characters, for displayed columns in the command line interpreter.

This is generally used to increase the default value in order to display large blocks of text.

Syntax

``` FcnSyntax
MAXIMUMDISPLAYWIDTH integer_value
```

integer\_value

The maximum width of each column that is displayed by the command line intepreter.

Set this value to <span class="CodeFont">0</span> to display the entire content of each column.

Examples

``` AppCommand
splice> maximumdisplaywidth 3;
splice> VALUES 'NOW IS THE TIME!';
1
---
NOW
splice> maximumdisplaywidth 30;
splice> VALUES 'NOW IS THE TIME!';
1
----------------
NOW IS THE TIME!
```

 


