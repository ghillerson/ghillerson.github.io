[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Extract.html)

[]()EXTRACT
===========

You can use the <span class="CodeFont">EXTRACT</span> built-in function can use to extract specific information from date and time values.

Syntax

``` FcnSyntax
EXTRACT( infoType FROM dateExpr );
```

infoType

The value (information) that you want to extract and return from the date-time expression. This can be one of the following values:

<span class="CodeFont">YEAR</span>

The four-digit year value is extracted from the date-time expression.

<span class="CodeFont">QUARTER</span>

The single digit (<span class="CodeFont">1-4</span>) quarter number is extracted from the date-time expression.

<span class="CodeFont">MONTH</span>

The month number (<span class="CodeFont">1-12</span>) is extracted from the date-time expression.

<span class="CodeFont">MONTHNAME</span>

The full month name (e.g. <span class="CodeFont">September</span>) is extracted from the date-time expression.

<span class="CodeFont">WEEK</span>

The week-of-year number (1 is the first week) is extracted from the date-time expression.

<span class="CodeFont">WEEKDAY</span>

The day-of-week number (<span class="CodeFont">1-7</span>, with Monday as <span class="CodeFont">1</span> and Sunday as <span class="CodeFont">7</span>) is extracted from the date-time expression.

<span class="CodeFont">WEEKDAYNAME</span>

The day-of-week name (e.g. <span class="CodeFont">Tuesday</span>)  is extracted from the date-time expression.

<span class="CodeFont">DAYOFYEAR</span>

The numeric day-of-year (<span class="CodeFont">0-366</span>) is extracted from the date-time expression.

<span class="CodeFont">DAY</span>

The numeric day-of-month (<span class="CodeFont">0-31</span>) is extracted from the date-time expression.

<span class="CodeFont">HOUR</span>

The numeric hour (<span class="CodeFont">0-23</span>) is extracted from the date-time expression.

Note that Splice Machine <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> values do not include time information and will not work correctly with this <span class="ItalicFont">infoType</span>.

<span class="CodeFont">MINUTE</span>

The numeric minute (<span class="CodeFont">0-59</span>) is extracted from the date-time expression.

Note that Splice Machine <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> values do not include time information and will not work correctly with this <span class="ItalicFont">infoType</span>.

<span class="CodeFont">SECOND</span>

The numeric second (<span class="CodeFont">0-59</span>) is extracted from the date-time expression.

Note that Splice Machine <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> values do not include time information and will not work correctly with this <span class="ItalicFont">infoType</span>.

dateExpr

The date-time expression from which you wish to extract information.

Note that Splice Machine <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> values do not include time information and thus will not produce correct values if you specify <span class="CodeFont">HOUR</span>, <span class="CodeFont">MINUTE</span>, or <span class="CodeFont">SECOND</span> infoTypes.

Examples

``` Example
splice> SELECT Birthdate, 
   EXTRACT (Quarter FROM Birthdate) "Quarter", 
   EXTRACT (Week FROM Birthdate) "Week", 
   EXTRACT(WeekDay FROM Birthdate) "Weekday" 
   FROM Players 
   WHERE ID < 20 
   ORDER BY "Quarter";
BIRTHDATE |Quarter    |Week       |Weekday    
----------------------------------------------
1987-03-27|1          |13         |5          
1987-01-21|1          |4          |3          
1991-01-15|1          |3          |2          
1982-01-05|1          |1          |2          
1990-03-22|1          |12         |4          
1989-01-01|1          |52         |7          
1988-04-20|2          |16         |3          
1983-04-13|2          |15         |3          
1990-06-16|2          |24         |6          
1984-04-11|2          |15         |3          
1981-07-02|3          |27         |4          
1977-08-30|3          |35         |2          
1989-08-21|3          |34         |1          
1984-09-21|3          |38         |5          
1990-10-30|4          |44         |2          
1983-12-24|4          |51         |6          
1983-11-06|4          |44         |7          
1982-10-12|4          |41         |2          
1989-11-17|4          |46         |5          

19 rows selected

splice> values EXTRACT(monthname FROM '2009-09-02 11:22:33.04');
1
--------------
September


splice> values EXTRACT(weekdayname FROM '2009-11-07 11:22:33.04');
1
--------------
Saturday
1 row selected

splice> values EXTRACT(dayofyear FROM '2009-02-01 11:22:33.04');
1
-----------
32
1 row selected

splice> values EXTRACT(hour FROM '2009-07-02 11:22:33.04');
1
-----------
11
1 row selected

splice> values EXTRACT(minute FROM '2009-07-02 11:22:33.04');
1
-----------
22
1 row selected

splice> values EXTRACT(second FROM '2009-07-02 11:22:33.04');
1
-----------
33

1 row selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
-   [<span class="CodeFont">DAY</span>](Day.html) function
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

 


