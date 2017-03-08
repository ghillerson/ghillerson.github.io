[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/ToChar.html)

[]()TO\_CHAR
============

The <span class="CodeFont">TO\_CHAR</span> function formats a date value into a string.

Syntax

``` FcnSyntax
TO_CHAR( dateExpr, format );
```

dateExpr

The date value that you want to format.

<span class="ItalicFont">format</span>

A string that specifies the format you want applied to the <span class="CodeFont">date</span>. You can specify formats such as the following:

yyyy-mm-dd

mm/dd/yyyy

dd.mm.yy

dd-mm-yy

Results

This function returns a string (<span class="CodeFont">CHAR</span>) value.

Examples

``` Example
splice> VALUES TO_CHAR(CURRENT_DATE, 'mm/dd/yyyy');
1 
----------------------------------------------------
09/22/2014
1 row selected

splice> VALUES TO_CHAR(CURRENT_DATE, 'dd-mm-yyyy');
1 
----------------------------------------------------
22-09-2014
1 row selected

splice> VALUES TO_CHAR(CURRENT_DATE, 'dd-mm-yy');
1 
----------------------------------------------------
22-09-14
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
-   [<span class="CodeFont">TO\_DATE</span>](ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


