[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Day.html)

<a href="" id="BuiltInFcns.Day"></a>[]()DAY
===========================================

The <span class="CodeFont">DAY</span> function returns the day part of a value.

Syntax

``` FcnSyntax
DAY ( expression )
```

expression

An expression that can be any of the following:

-   A [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) value
-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A valid string representation of a date or timestamp that is not a [<span class="CodeFont">CLOB</span>](../DataTypes/Clob.html) or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) value.

Results

The returned result is an integer value in the range <span class="CodeFont">1</span> to <span class="CodeFont">31</span>.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span> value.

Examples

Get the current date:

``` Example
splice> VALUES(CURRENT_DATE);
1
--------
2015-10-25

1 row selected
```

Now get the current day only:

``` Example
splice> VALUES(DAY(CURRENT_DATE));
1
--------
25

1 row selected
```

Get the day number for each player's birthdate:

``` Example
splice> select Day(Birthdate) AS "Day-of-Birth"
   FROM Players 
   WHERE ID < 20 
   ORDER BY "Day-of-Birth";
Day-of-Bir&
-----------
1          
2          
5          
6          
11         
12         
13         
15         
16         
17         
20         
21         
21         
21         
22         
24         
27         
30         
30         

19 rows selected
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) data type
-   [<span class="CodeFont">DATE</span>](Date.html) function
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

 


