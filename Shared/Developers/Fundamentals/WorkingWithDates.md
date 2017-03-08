[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/WorkingWithDates.html)

Working With Date and Time Values
=================================

This topic provides an overview of working with dates in Splice Machine.

For date and time values to work as expected in your database, you must make sure that all nodes in your cluster are set to the same time zone; otherwise the data you read from your database may differ, when you communicate with different servers!
Please contact your system administrator if you have any questions about this.

Date and Time Functions
-----------------------

Here is a summary of the  <span class="CodeFont">[DATE](../../SQLReference/DataTypes/Date.html)</span>, <span class="CodeFont">[TIME](../../SQLReference/DataTypes/Time.html)</span>, and <span class="CodeFont">[TIMESTAMP](../../SQLReference/DataTypes/TimeStamp.html)</span> functions included in this release of Splice Machine:

| Function                                                           | Description                                                                                                                                                                                                                                                                    |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [CURRENT\_DATE](../../SQLReference/BuiltInFcns/CurrentDate.html)   | Returns the current date as a <span class="CodeFont">DATE</span> value.                                                                                                                                                                                                        |
| [DATE](../../SQLReference/BuiltInFcns/Date.html)                   | Returns a <span class="CodeFont">DATE</span> value from a <span class="CodeFont">DATE</span> value, a <span class="CodeFont">TIMESTAMP</span> value, a string representation of a date or timestamp value, or a numeric value representing elapsed days since January 1, 1970. |
| [DAY](../../SQLReference/BuiltInFcns/Day.html)                     | Returns an integer value between 1 and 31 representing the day portion of a <span class="CodeFont">DATE</span> value, a <span class="CodeFont">TIMESTAMP</span> value, or a string representation of a date or timestamp value.                                                |
| [EXTRACT](../../SQLReference/BuiltInFcns/Extract.html)             | Extracts various date and time components from a date expression.                                                                                                                                                                                                              |
| [LAST\_DAY](../../SQLReference/BuiltInFcns/LastDay.html)           | Returns a <span class="CodeFont">DATE</span> value representing the date of the last day of the month that contains the input date.                                                                                                                                            |
| [MONTH](../../SQLReference/BuiltInFcns/Month.html)                 | Returns an integer value between 1 and 12 representing the month portion of a <span class="CodeFont">DATE</span> value, a <span class="CodeFont">TIMESTAMP</span> value, or a string representation of a date or timestamp value.                                              |
| [MONTH\_BETWEEN](../../SQLReference/BuiltInFcns/MonthBetween.html) | Returns a decimal number representing the number of months between two dates.                                                                                                                                                                                                  |
| [MONTHNAME](../../SQLReference/BuiltInFcns/MonthName.html)         | Returns the month name from a date expression.                                                                                                                                                                                                                                 |
| [NEXT\_DAY](../../SQLReference/BuiltInFcns/NextDay.html)           | Returns the date of the next specified day of the week after a specified date.                                                                                                                                                                                                 |
| [NOW](../../SQLReference/BuiltInFcns/Now.html)                     | Returns the current date and time as a <span class="CodeFont">TIMESTAMP</span> value.                                                                                                                                                                                          |
| [QUARTER](../../SQLReference/BuiltInFcns/Quarter.html)             | Returns the quarter number (1-4) from a date expression.                                                                                                                                                                                                                       |
| [TIMESTAMP](../../SQLReference/BuiltInFcns/TimeStamp.html)         | Returns a timestamp value from a <span class="CodeFont">TIMESTAMP</span> value, a string representation of a timestamp value, or a string of digits representing such a value.                                                                                                 |
| [TIMESTAMPADD](../../SQLReference/BuiltInFcns/TimeStampAdd.html)   | Adds the value of an interval to a <span class="CodeFont">TIMESTAMP</span> value and returns the sum as a new timestamp.                                                                                                                                                       |
| [TIMESTAMPDIFF](../../SQLReference/BuiltInFcns/TimeStampDiff.html) | Finds the difference between two timestamps, in terms of the specfied interval.                                                                                                                                                                                                |
| [TO\_CHAR](../../SQLReference/BuiltInFcns/ToChar.html)             | Returns string formed from a DATE value, using a format specification.                                                                                                                                                                                                         |
| [TO\_DATE](../../SQLReference/BuiltInFcns/ToDate.html)             | Returns a <span class="CodeFont">DATE</span> value formed from an input string representation, using a format specification.                                                                                                                                                   |
| [WEEK](../../SQLReference/BuiltInFcns/Week.html)                   | Returns the week number (1-53) from a date expression.                                                                                                                                                                                                                         |
| [YEAR](../../SQLReference/BuiltInFcns/Year.html)                   | Returns an integer value between 1 and 9999 representing the year portion of a <span class="CodeFont">DATE</span> value, a <span class="CodeFont">TIMESTAMP</span> value, or a string representation of a date or timestamp value.                                             |

Date Arithmetic
---------------

Splice Machine provides simple arithmetic operations — addition and subtraction — on date and timestamp values. You can:

-   find a future date value by adding an integer number of days to a date value
-   find a past date value by subtracting an integer number of days from a date value
-   subtract two date values to find the difference, in days, between those two values

Here's the syntax for these inline operations:

``` FcnSyntax
   dateValue { "+" | "-" } numDays
|  numDays   '+' dateValue
|  dateValue '-' dateValue
```

dateValue

A <span class="CodeFont">[DATE](../../SQLReference/DataTypes/Date.html)</span> value or a <span class="CodeFont">[TIMESTAMP](../../SQLReference/DataTypes/TimeStamp.html)</span> value. This can be a literal date value, a reference to a date value in a table, or the result of a function that produces a date value as its result.

numDays

An integer value expressing the number of days to add or subtract to a date value.

### Result Types

The result type of adding or subtracting a number of days to/from a date value is a date value of the same type (<span class="CodeFont">DATE</span> or <span class="CodeFont">TIMESTAMP</span>) as the <span class="CodeFont">dateValue</span> operand.

The result type of subtracting one date value from another is the number of days between the two dates. This can be a positive or negative integer value.

### Notes

A few important notes about these operations:

-   Adding a number of days to a date value is commutative, which means that the order of the <span class="CodeFont">dateValue</span> and <span class="CodeFont">numDays</span> operands is irrelevant.
-   Subtraction of a number of days from a date value is not commutative: the left-side operand must be a date value.
-   Attempting to add two date values produces an error, as does attempting to use a date value in a multiplication or division operation.

### Examples

This section presents several examples of using date arithmetic. We'll first set up a simple table that stores a string value, a <span class="CodeFont">DATE</span> value, and a <span class="CodeFont">TIMESTAMP</span> value, and we'll use those values in our example.

``` Example
splice> CREATE TABLE date_math (s VARCHAR(30), d DATE, t TIMESTAMP);
0 rows inserted/updated/deleted

splice> INSERT INTO date_math values ('2012-05-23 12:24:36', '1988-12-26', '2000-06-07 17:12:30');
1 row inserted/updated/deleted
```

#### Example 1: Add a day to a date column and then to a timestamp column

``` Example
splice> select d + 1 from date_math;
1
----------
1988-12-27
1 row selected

splice> select 1+t from date_math;
1
----------
2000-06-08 17:12:30.0
1 row selected
```

#### Example 2: Subtract a day from a timestamp column

``` Example
splice> select t - 1 from date_math;
1
-----------------------------
2000-06-06 17:12:30.0
1 row selected
```

#### Example 3: Subtract a date column from the result of the <span class="CodeFont">CURRENT\_DATE</span> function

``` Example
splice> select current_date - d from date_math;
1
-----------
9551
1 row selected
```

#### Example 4: Additional examples using literal values

``` Example
splice> values  date('2011-12-26') + 1;
1
----------
2011-12-27
1 row selected

splice> values  date('2011-12-26') - 1;
1
----------
2011-12-25
1 row selected

splice> values  timestamp('2011-12-26', '17:13:30') + 1;
1
-----------------------------
2011-12-27 17:13:30.0
1 row selected

splice> values  timestamp('2011-12-26', '17:13:30') - 1;
1
-----------------------------
2011-12-25 17:13:30.0
1 row selected

splice> values  date('2011-12-26') - date('2011-06-05');
1
-----------
204
1 row selected

splice> values  date('2011-06-05') - date('2011-12-26');
1
-----------
-204
1 row selected


splice> values  timestamp('2015-06-07', '05:06:00') - current_date;
1
-----------
108
1 row selected

splice> values  timestamp('2011-06-05', '05:06:00') - date('2011-12-26');
1
-----------
-203
1 row selected
```

See Also
--------

All of the following are in the <span class="ItalicFont">[SQL Reference Manual](../../SQLReference/Intro.SQLReference.html)</span>:

-   [<span class="CodeFont">CURRENT\_DATE</span>](../../SQLReference/BuiltInFcns/CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../../SQLReference/DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](../../SQLReference/BuiltInFcns/Date.html) function
-   [<span class="CodeFont">DAY</span>](../../SQLReference/BuiltInFcns/Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](../../SQLReference/BuiltInFcns/Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](../../SQLReference/BuiltInFcns/LastDay.html) function
-   [<span class="CodeFont">MONTH</span>](../../SQLReference/BuiltInFcns/Month.html) function
-   [<span class="CodeFont">MONTH\_BETWEEN</span>](../../SQLReference/BuiltInFcns/MonthBetween.html) function
-   [<span class="CodeFont">MONTHNAME</span>](../../SQLReference/BuiltInFcns/MonthName.html) function
-   [<span class="CodeFont">NEXTDAY</span>](../../SQLReference/BuiltInFcns/NextDay.html) function
-   [<span class="CodeFont">NOW</span>](../../SQLReference/BuiltInFcns/Now.html) function
-   [<span class="CodeFont">QUARTER</span>](../../SQLReference/BuiltInFcns/Quarter.html) function
-   [<span class="CodeFont">TIME</span>](../../SQLReference/DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](../../SQLReference/BuiltInFcns/TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](../../SQLReference/BuiltInFcns/ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](../../SQLReference/BuiltInFcns/ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](../../SQLReference/BuiltInFcns/Week.html) function

 


