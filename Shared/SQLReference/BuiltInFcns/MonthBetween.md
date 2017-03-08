[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/MonthBetween.html)

[]()MONTH\_BETWEEN
==================

The <span class="CodeFont">MONTH\_BETWEEN</span> function returns the number of months between two dates.

Syntax

``` FcnSyntax
MONTH_BETWEEN( date1, date2 );
```

date1

The first date.

date2

The second date

Results

If <span class="CodeFont">date1</span> is later than <span class="CodeFont">date2</span>, then the result is positive.

If <span class="CodeFont">date1</span> is earlier than <span class="CodeFont">date2</span>, then the result is negative.

If <span class="CodeFont">date1</span> and <span class="CodeFont">date2</span> are either the same days of the month or both last days of months, then the result is always an integer.

Examples

``` Example
splice> VALUES(MONTH_BETWEEN(CURRENT_DATE, DATE('2015-8-15')));
1 
----------------------
3.0

splice> SELECT MIN(BirthDate) "Oldest", 
   MAX(Birthdate) "Youngest", 
   MONTH_BETWEEN(MIN(Birthdate), MAX(BirthDate)) "Months Between" 
   FROM Players; 
Oldest     |Youngest   |Months Between 
--------------------------------------------
1975-07-14 |1992-10-19 |207.0

1 row selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](LastDay.html) function
-   [<span class="CodeFont">MONTH</span>](Month.html) function
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

 


