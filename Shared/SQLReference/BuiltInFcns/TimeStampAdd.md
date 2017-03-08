[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/TimeStampAdd.html)

<a href="" id="BuiltInFcns.TimeStamp"></a>[]()TIMESTAMPADD
==========================================================

The <span class="CodeFont">TIMESTAMPADD</span> function adds the value of an interval to a timestamp value and returns the sum as a new timestamp. You can supply a negative interval value to substract from a timestamp.

Syntax

``` FcnSyntax
TIMESTAMPADD ( interval, count, timeStamp1 )
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

count

An integer specifying the number of times the interval is to be added to the timestamp. Use a negative integer value to subtract.

timeStamp1

The [timestamp](../DataTypes/TimeStamp.html) value to which the count of intervals is added.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you use a <span class="CodeFont">datetime</span> column inside the <span class="CodeFont">TIMESTAMPADD</span> function in a <span class="CodeFont">WHERE</span> clause, the optimizer cannot use indexes on that column. We strongly recommend not doing this!

Results

The <span class="CodeFont">TIMESTAMPADD</span> function returns a [timestamp](../DataTypes/TimeStamp.html) value that is the result of adding <span class="ItalicFont">count intervals</span> to <span class="ItalicFont">timeStamp1</span>.

Examples

The following example displays the current timestamp, and the timestamp value two months from now:

``` Example
splice> VALUES ( CURRENT_TIMESTAMP, TIMESTAMPADD(SQL_TSI_MONTH, 2, CURRENT_TIMESTAMP ));
1                            |2                            
-----------------------------------------------------------
2015-11-23 13:54:16.728      |2016-01-23 13:54:16.728      

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) data value
-   [<span class="CodeFont">HOUR</span>](Hour.html) function
-   [<span class="CodeFont">MINUTE</span>](Minute.html) function
-   [<span class="CodeFont">SECOND</span>](Second.html) function
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TIMESTAMPDIFF</span>](TimeStampDiff.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


