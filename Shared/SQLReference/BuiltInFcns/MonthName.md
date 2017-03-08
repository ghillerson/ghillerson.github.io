[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/MonthName.html)

MONTHNAME
=========

The <span class="CodeFont">MONTHNAME</span> function returns a character string containing month name from a date expression.

Syntax

``` FcnSyntax
MONTHNAME( dateExpr );
```

dateExpr

The date-time expression from which you wish to extract information.

Results

The returned month name is specific to the data source location; for English, the returned name will be in the range <span class="CodeFont">January</span> through <span class="CodeFont">December</span>, or <span class="CodeFont">Jan.</span> through <span class="CodeFont">Dec.</span> For a data source that uses German, the returned name will be in the range <span class="CodeFont">Januar</span> through <span class="CodeFont">Dezember</span>.

Examples

The following query displays the birth month of players:

``` Example
splice> SELECT DisplayName, MONTHNAME(BirthDate) "Month"
   FROM Players
   WHERE ID<20
   ORDER BY MONTH(BirthDate);
DISPLAYNAME             |Month         
---------------------------------------
Bob Cranker             |January       
Mitch Duffer            |January       
Norman Aikman           |January       
Jeremy Packman          |January       
Buddy Painter           |March         
Andy Sussman            |March         
Billy Bopper            |April         
Harry Pennello          |April         
Alex Darba              |April         
Kelly Tamlin            |June          
Alex Paramour           |July          
Mark Briste             |August        
Elliot Andrews          |August        
Joseph Arkman           |September     
John Purser             |October       
Craig McGawn            |October       
Jason Minman            |November      
Henry Socomy            |November      
Greg Brown              |December      

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
-   [<span class="CodeFont">NEXTDAY</span>](NextDay.html) function
-   [<span class="CodeFont">NOW</span>](Now.html) function
-   [<span class="CodeFont">QUARTER</span>](Quarter.html) function
-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


