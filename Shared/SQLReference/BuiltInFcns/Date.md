[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Date.html)

<a href="" id="BuiltInFcns.Date"></a>[]()DATE
=============================================

The <span class="CodeFont">DATE</span> function returns a date from a value.

Syntax

``` FcnSyntax
DATE ( expression )
```

expression

An expression that can be any of the following:

-   A [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) value
-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A positive number less than or equal to 2,932,897
-   A valid SQL string representation of a date or timestamp
-   A string of length 7 that is not a [<span class="CodeFont">CLOB</span>](../DataTypes/Clob.html) or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) value, which must represent a valid date in the form <span class="CodeFont">yyyynnn</span>, where <span class="CodeFont">yyyy</span> is a four-digit year value, and <span class="CodeFont">nnn</span> is a three-digit day value in the range 001 to 366.

Results

The returned result is governed by the following rules:

-   If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span> value.
-   If the argument is a date, timestamp, or valid string representation of a date or timestamp, the result is the date part of the value.
-   If the argument is a number, the result is the date that is <span class="CodeFont">n-1</span> days after January 1, 1970, where <span class="CodeFont">n</span> is the integral part of the number.
-   If the argument is a string with a length of 7, the result is a string representation of the date.

Examples

This example results in an internal representation of '1988-12-25'.

``` Example
splice> VALUES DATE('1988-12-25');
```

This example results in an internal representation of '1972-02-28'.

``` Example
splice> VALUES DATE(789);
```

This example illustrates using date arithmetic with the <span class="CodeFont">DATE</span> function:

``` Example
splice> select Birthdate - DATE('11/22/1963') AS "DaysSinceJFK" FROM Players WHERE ID < 20;
DaysSinceJ&
-----------
8526       
8916       
9839       
8461       
9916       
6619       
6432       
7082       
7337       
7289       
9703       
5030       
9617       
6899       
9404       
7446       
7609       
9492       
9172       

19 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](LastDay.html) function
-   [<span class="CodeFont">MONTH</span>](Month.html) function
-   [<span class="CodeFont">MONTH\_BETWEEN</span>](MonthBetween.html) function
-   [<span class="CodeFont">MONTHNAME</span>](MonthName.html) function
-   [<span class="CodeFont">NEXTDAY</span>](NextDay.html) function
-   [<span class="CodeFont">NOW</span>](Now.html) function
-   [<span class="CodeFont">QUARTER</span>](Quarter.html) function
-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


