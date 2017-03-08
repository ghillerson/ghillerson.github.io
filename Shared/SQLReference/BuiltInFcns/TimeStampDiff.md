[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/TimeStampDiff.html)

<a href="" id="BuiltInFcns.TimeStamp"></a>[]()TIMESTAMPDIFF
===========================================================

The <span class="CodeFont">TIMESTAMPDIFF</span> function finds the difference between two timestamps, in terms of the specfied interval.

Syntax

``` FcnSyntax
TIMESTAMPDIFF ( interval, timeStamp1, timeStamp2 )
```

interval

One of the following timestamp interval constants:

-   SQL\_TSI\_FRAC\_SECOND
-   SQL\_TSI\_SECOND
-   SQL\_TSI\_MINUTE
-   SQL\_TSI\_HOUR
-   SQL\_TSI\_DAY
-   SQL\_TSI\_WEEK,
-   SQL\_TSI\_MONTH
-   SQL\_TSI\_QUARTER
-   SQL\_TSI\_YEAR

timeStamp1

The first [timestamp](../DataTypes/TimeStamp.html) value.

timeStamp2

The second [timestamp](../DataTypes/TimeStamp.html) value.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you use a <span class="CodeFont">datetime</span> column inside the <span class="CodeFont">TIMESTAMPDIFF</span> function in a <span class="CodeFont">WHERE</span> clause, the optimizer cannot use indexes on that column. We strongly recommend not doing this!

Results

The <span class="CodeFont">TIMESTAMPDIFF</span> function returns an integer value representing the count of intervals between the two timestamp values.

Examples

These examples shows the number of years a player was born after Nov 22, 1963:.

``` Example
splice> SELECT ID, BirthDate, TIMESTAMPDIFF(SQL_TSI_YEAR, Date('11/22/1963'), BirthDate) "YearsSinceJFK"
   FROM Players WHERE ID < 11
   ORDER BY Birthdate;
ID    |BIRTHDATE |YearsSinceJFK       
--------------------------------------
7     |1981-07-02|17                  
6     |1982-01-05|18                  
8     |1983-04-13|19                  
10    |1983-11-06|19                  
9     |1983-12-24|20                  
4     |1987-01-21|23                  
1     |1987-03-27|23                  
2     |1988-04-20|24                  
3     |1990-10-30|26                  
5     |1991-01-15|27                  

10 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) data value
-   [<span class="CodeFont">HOUR</span>](Hour.html) function
-   [<span class="CodeFont">MINUTE</span>](Minute.html) function
-   [<span class="CodeFont">SECOND</span>](Second.html) function
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TIMESTAMPADD</span>](TimeStampAdd.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


