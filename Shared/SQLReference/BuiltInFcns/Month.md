[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Month.html)

<a href="" id="BuiltInFcns.Month"></a>[]()MONTH
===============================================

The <span class="CodeFont">MONTH</span> function returns the month part of a value.

Syntax

``` FcnSyntax
MONTH ( expression )
```

expression

An expression that can be any of the following:

-   A [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) value
-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A valid string representation of a date or timestamp that is not a [<span class="CodeFont">CLOB</span>](../DataTypes/Clob.html) or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) value.

Results

The returned result is an integer value in the range <span class="CodeFont">1</span> to <span class="CodeFont">12</span>.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span> value.

Examples

Get the current date:

``` Example
splice> VALUES(CURRENT_DATE);
1
--------
2014-05-15
```

Now get the current month only:

``` Example
splice> VALUES(MONTH(CURRENT_DATE));
1
--------
5
```

Get the month of one week from now:

``` Example
splice> VALUES(MONTH(CURRENT_DATE+7));
1
--------
5
```

Select all players who were born in December:

``` Example
splice> SELECT DisplayName, Team, BirthDate 
   FROM Players 
   WHERE MONTH(BirthDate)=12;
DISPLAYNAME             |TEAM      |BIRTHDATE 
----------------------------------------------
Greg Brown              |Giants    |1983-12-24
Reed Lister             |Giants    |1986-12-16
Cameron Silliman        |Cards     |1988-12-21
Edward Erdman           |Cards     |1985-12-21
Taylor Trantula         |Cards     |1987-12-17
Tam Croonster           |Cards     |1980-12-19

6 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](LastDay.html) function
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

 


