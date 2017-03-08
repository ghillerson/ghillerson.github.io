[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Quarter.html)

QUARTER
=======

The <span class="CodeFont">QUARTER</span> function returns an integer value representing the quarter of the year from a date expression.

Syntax

``` FcnSyntax
QUARTER( dateExpr );
```

dateExpr

The date-time expression from which you wish to extract information.

Results

The returned week number is in the range <span class="CodeFont">1</span> to <span class="CodeFont">4</span>. January 1 through March 31 is Quarter <span class="CodeFont">1</span>.

Examples

``` Example
splice> VALUES QUARTER('2009-01-02 11:22:33.04');
1
-----------
1
1 row selected

splice> SELECT DisplayName, BirthDate, Quarter(BirthDate) "Quarter" 
   FROM Players 
   WHERE ID<20 
   ORDER BY "Quarter", BirthDate;
DISPLAYNAME             |BIRTHDATE |Quarter    
-----------------------------------------------
Norman Aikman           |1982-01-05|1          
Bob Cranker             |1987-01-21|1          
Buddy Painter           |1987-03-27|1          
Jeremy Packman          |1989-01-01|1          
Andy Sussman            |1990-03-22|1          
Mitch Duffer            |1991-01-15|1          
Harry Pennello          |1983-04-13|2          
Alex Darba              |1984-04-11|2          
Billy Bopper            |1988-04-20|2          
Kelly Tamlin            |1990-06-16|2          
Mark Briste             |1977-08-30|3          
Alex Paramour           |1981-07-02|3          
Joseph Arkman           |1984-09-21|3          
Elliot Andrews          |1989-08-21|3          
Craig McGawn            |1982-10-12|4          
Jason Minman            |1983-11-06|4          
Greg Brown              |1983-12-24|4          
Henry Socomy            |1989-11-17|4          
John Purser             |1990-10-30|4          

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
-   [<span class="CodeFont">NEXTDAY</span>](NextDay.html) function
-   [<span class="CodeFont">NOW</span>](Now.html) function
-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


