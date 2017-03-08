[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/NextDay.html)

[]()NEXT\_DAY
=============

The <span class="CodeFont">NEXT\_DAY</span> function returns the date of the next specified day of the week after a specified date.

Syntax

``` FcnSyntax
NEXT_DAY( source_date, day_of_week);
```

source\_date

The source date.

day\_of\_week

The day of the week. This is the case-insensitive name of a day in the date language of your session. You can also specify day-name abbreviations, in which case any characters after the recognized abbreviation are ignored. For example, if you're using English, you can use the following values (again, the case of the characters is ignored):

| Day Name  | Abbreviation |
|-----------|--------------|
| Sunday    | Sun          |
| Monday    | Mon          |
| Tuesday   | Tue          |
| Wednesday | Wed          |
| Thursday  | Thu          |
| Friday    | Fri          |
| Saturday  | Sat          |

Results

This function returns the date of the first weekday, as specified by <span class="CodeFont">day\_of\_week</span>, that is later than the specified date.

The return type is always <span class="CodeFont">DATE</span>, regardless of the data type of the <span class="CodeFont">source\_date</span> parameter.

The return value has the same hours, minutes, and seconds components as does the <span class="CodeFont">source\_date</span> parameter value.

Examples

``` Example
splice> values (NEXT_DAY(CURRENT_DATE, 'tuesday'));
1 
----------
2014-09-23
1 row selected

splice> values (NEXT_DAY(CURRENT_DATE, 'monday'));
1
----------
2014-09-29
1 row selected

SELECT DisplayName, BirthDate, NEXT_DAY(BirthDate, 'sunday') as "FirstSunday" 
   FROM Players
   WHERE ID < 20;
DISPLAYNAME             |BIRTHDATE |FirstSund&
----------------------------------------------
Buddy Painter           |1987-03-27|1987-03-29
Billy Bopper            |1988-04-20|1988-04-24
John Purser             |1990-10-30|1990-11-04
Bob Cranker             |1987-01-21|1987-01-25
Mitch Duffer            |1991-01-15|1991-01-20
Norman Aikman           |1982-01-05|1982-01-10
Alex Paramour           |1981-07-02|1981-07-05
Harry Pennello          |1983-04-13|1983-04-17
Greg Brown              |1983-12-24|1983-12-25
Jason Minman            |1983-11-06|1983-11-06
Kelly Tamlin            |1990-06-16|1990-06-17
Mark Briste             |1977-08-30|1977-09-04
Andy Sussman            |1990-03-22|1990-03-25
Craig McGawn            |1982-10-12|1982-10-17
Elliot Andrews          |1989-08-21|1989-08-27
Alex Darba              |1984-04-11|1984-04-15
Joseph Arkman           |1984-09-21|1984-09-23
Henry Socomy            |1989-11-17|1989-11-19
Jeremy Packman          |1989-01-01|1989-01-01

19 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](LastDay.html) function
-   [<span class="CodeFont">MONTH</span>](Month.html) function
-   [<span class="CodeFont">MONTH\_BETWEEN</span>](MonthBetween.html) function
-   [<span class="CodeFont">MONTHNAME</span>](MonthName.html) function
-   [<span class="CodeFont">NOW</span>](Now.html) function
-   [<span class="CodeFont">QUARTER</span>](Quarter.html) function
-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


