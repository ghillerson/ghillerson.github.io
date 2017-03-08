[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Week.html)

WEEK
====

The <span class="CodeFont">WEEK</span> function returns an integer value representing the week of the year from a date expression.

Syntax

``` FcnSyntax
WEEK( dateExpr );
```

dateExpr

The date-time expression from which you wish to extract information.

Results

The returned week number is in the range <span class="CodeFont">1</span> to <span class="CodeFont">53</span>.

Examples

``` Example
splice> SELECT BirthDate, Week(BirthDate) "BirthWeek"
   FROM Players 
   WHERE ID < 15;
BIRTHDATE |BIRTHWEEK
----------------------
1987-03-27|13         
1988-04-20|16         
1990-10-30|44         
1987-01-21|4          
1991-01-15|3          
1982-01-05|1          
1981-07-02|27         
1983-04-13|15         
1983-12-24|51         
1983-11-06|44         
1990-06-16|24         
1977-08-30|35         
1990-03-22|12         
1982-10-12|41         

14 rows selected
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
-   [<span class="CodeFont">QUARTER</span>](Quarter.html) function
-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


