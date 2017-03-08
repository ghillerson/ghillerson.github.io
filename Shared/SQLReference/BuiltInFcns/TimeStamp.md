[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/TimeStamp.html)

<a href="" id="BuiltInFcns.TimeStamp"></a>[]()TIMESTAMP
=======================================================

The <span class="CodeFont">TIMESTAMP</span> function returns a timestamp from a value or a pair of values.

Syntax

``` FcnSyntax
TIMESTAMP ( expression1 [, expression2 ] )
```

expression1

If <span class="ItalicFont">expression2</span> is also specified, <span class="ItalicFont">expression1</span> must be a date or a valid string representation of a date.

If only <span class="ItalicFont">expression1</span> is specified, it must be one of the following:

-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> value
-   A valid SQL string representation of a timestamp

expression2

(Optional). A time or a valid string representation of a time.

Results

The data type of the result depends on how the input expression(s) were specified:

-   If both <span class="ItalicFont">expression1</span> and <span class="ItalicFont">expression2</span> are specified, the result is a timestamp with the date specified by <span class="ItalicFont">expression1</span> and the time specified by <span class="ItalicFont">expression2</span>. The microsecond part of the timestamp is zero.
-   If only <span class="ItalicFont">expression1</span> is specified and it is a timestamp, the result is that timestamp.
-   If only <span class="ItalicFont">expression1</span> is specified and it is a string, the result is the timestamp represented by that string. If <span class="ItalicFont">expression1</span> is a string of length 14, the timestamp has a microsecond part of zero.

Examples

This example converts date and time strings into a timestamp value:

``` Example
splice> VALUES TIMESTAMP('2015-11-12', '19:02:43');
1                            
-----------------------------
2015-11-12 19:02:43.0        

1 row selected
```

This query shows the timestamp version of the birth date of each player born in the final quarter of the year:

``` Example
splice> SELECT TIMESTAMP(BirthDate) 
   FROM Players 
   WHERE MONTH(BirthDate) > 10 
   ORDER BY BirthDate;
1                            
-----------------------------
1980-12-19 00:00:00.0        
1983-11-06 00:00:00.0        
1983-11-28 00:00:00.0        
1983-12-24 00:00:00.0        
1984-11-22 00:00:00.0        
1985-11-07 00:00:00.0        
1985-11-26 00:00:00.0        
1985-12-21 00:00:00.0        
1986-11-13 00:00:00.0        
1986-11-24 00:00:00.0        
1986-12-16 00:00:00.0        
1987-11-12 00:00:00.0        
1987-11-16 00:00:00.0        
1987-12-17 00:00:00.0        
1988-12-21 00:00:00.0        
1989-11-17 00:00:00.0        
1991-11-15 00:00:00.0        

17 rows selected
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
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


