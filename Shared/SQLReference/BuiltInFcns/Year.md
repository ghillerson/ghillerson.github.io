[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Year.html)

<a href="" id="BuiltInFcns.Year"></a>[]()YEAR
=============================================

The <span class="CodeFont">YEAR</span> function returns the year part of a value. The argument must be a date, timestamp, or a valid character string representation of a date or timestamp. The result of the function is an integer between <span class="CodeFont">1</span> and <span class="CodeFont">9999</span>.

Syntax

``` FcnSyntax
YEAR ( expression )
```

Usage

If the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span> value.

Examples

Get the current date:

``` Example
splice> value(current_date);
1
--------
2014-02-25
```

Now get the current year only:

``` Example
splice> value(year(current_date));
1
--------
2015
```

Now get the year value from 60 days ago:

``` Example
splice> value(year(current_date-60));
1
--------
2014
```

Select all players born in 1985 or 1989:

``` Example
splice> SELECT DisplayName, Team, BirthDate 
   FROM Players 
   WHERE YEAR(BirthDate) IN (1985, 1989) 
   ORDER BY BirthDate;
DISPLAYNAME             |TEAM     |BIRTHDATE 
-----------------------------------------------
Jeremy Johnson          |Cards    |1985-03-15
Gary Kosovo             |Giants   |1985-06-12
Michael Hillson         |Cards    |1985-11-07
Mitch Canepa            |Cards    |1985-11-26
Edward Erdman           |Cards    |1985-12-21
Jeremy Packman          |Giants   |1989-01-01
Nathan Nickels          |Giants   |1989-05-04
Ken Straiter            |Cards    |1989-07-20
Marcus Bamburger        |Giants   |1989-08-01
George Goomba           |Cards    |1989-08-08
Jack Hellman            |Cards    |1989-08-09
Elliot Andrews          |Giants   |1989-08-21
Henry Socomy            |Giants   |1989-11-17

13 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">LASTDAY</span>](LastDay.html) function
-   <span class="CodeFont">[MONTH](Month.html)</span> function
-   [<span class="CodeFont">MONTH\_BETWEEN</span>](MonthBetween.html) function
-   [<span class="CodeFont">NEXTDAY</span>](NextDay.html) function
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


