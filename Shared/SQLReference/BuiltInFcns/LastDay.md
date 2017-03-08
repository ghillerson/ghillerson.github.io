[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/LastDay.html)

[]()LAST\_DAY
=============

The <span class="CodeFont">LAST\_DAY</span> function returns the date of the last day of the month that contains the input date.

Syntax

``` FcnSyntax
LAST_DAY ( dateExpression )
```

dateExpression

A date value.

Results

The return type is always <span class="CodeFont">[DATE](../DataTypes/Date.html)</span>, regardless of the data type of the <span class="ItalicFont">dateExpression</span>.

Examples

``` Example
Examples:
splice> values (LAST_DAY(CURRENT_DATE));
1 
----------
2015-11-30

splice> values (LAST_DAY(DATE(CURRENT_TIMESTAMP)));
1 
----------
2015-11-30

splice> SELECT DISPLAYNAME, BirthDate, LAST_DAY(BirthDate) "MonthEnd" 
   FROM Players  
   WHERE MONTH(BirthDate) IN (2, 5, 12);
DISPLAYNAME             |BIRTHDATE |MonthEnd  
----------------------------------------------
Tam Croonster           |1980-12-19|1980-12-31
Jack Peepers            |1981-05-31|1981-05-31
Jason Martell           |1982-02-01|1982-02-28
Kameron Fannais         |1982-05-24|1982-05-31
Jonathan Pearlman       |1982-05-28|1982-05-31
Greg Brown              |1983-12-24|1983-12-31
Edward Erdman           |1985-12-21|1985-12-31
Jonathan Wilson         |1986-05-14|1986-05-31
Reed Lister             |1986-12-16|1986-12-31
Larry Lintos            |1987-05-12|1987-05-31
Taylor Trantula         |1987-12-17|1987-12-31
Tim Lentleson           |1988-02-21|1988-02-29
Cameron Silliman        |1988-12-21|1988-12-31
Nathan Nickels          |1989-05-04|1989-05-31
Tom Rather              |1990-05-29|1990-05-31
Mo Grandosi             |1992-02-16|1992-02-29

16 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](Extract.html) function
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

 


