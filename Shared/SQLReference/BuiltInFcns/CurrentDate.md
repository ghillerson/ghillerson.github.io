[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentDate.html)

<a href="" id="BuiltInFcns.CurrentDate"></a>[]()CURRENT\_DATE
=============================================================

<span class="CodeFont">CURRENT\_DATE</span> returns the current date.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> This function returns the same value if it is executed more than once in a single statement, which means that the value is fixed, even if there is a long delay between fetching rows in a cursor.

Syntax

``` FcnSyntax
CURRENT_DATE
```

or, alternately

``` FcnSyntax
CURRENT DATE
```

Results

A <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> value.

Examples

The following query finds all players older that 33 years (as of Nov. 9, 2015) on the Cards baseball team:

``` Example
splice> SELECT displayName, birthDate
   FROM Players
   WHERE (BirthDate+(33 * 365.25)) <= CURRENT_DATE AND Team='Cards';
DISPLAYNAME             |BIRTHDATE 
-----------------------------------
Yuri Milleton           |1982-07-13
Jonathan Pearlman       |1982-05-28
David Janssen           |1979-08-10
Jason Larrimore         |1978-10-23
Tam Croonster           |1980-12-19
Alex Wister             |1981-08-30
Robert Cohen            |1975-09-05
Mitch Brandon           |1980-06-06

8 rows selected
```

See Also

-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
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

 


