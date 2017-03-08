[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Time.html)

<a href="" id="DataTypes.Time"></a>[]()TIME
===========================================

The <span class="CodeFont">TIME</span> data type provides for storage of a time-of-day value.

Syntax

``` FcnSyntax
TIME
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.sql.Time
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
TIME
```

Usage Notes

Here are several usage notes for the <span class="CodeFont">TIME</span> data type:

-   [Dates](Date.html), times, and [timestamps](TimeStamp.html) cannot be mixed with one another in expressions except with a <span class="CodeFont">CAST</span>.
-   Any value that is recognized by the <span class="ItalicFont">java.sql.Time</span> method is permitted in a column of the corresponding SQL date/time data type. Splice Machine supports the following formats for <span class="CodeFont">TIME</span>:

    ``` FcnSyntax
    hh:mm[:ss]
    hh.mm[.ss]
    hh[:mm] {AM | PM}
    ```

    The first of the three formats above is the <span class="ItalicFont">java.sql.Time</span> format.

-   Hours may have one or two digits.
-   Minutes and seconds, if present, must have two digits.
-   Splice Machine also accepts strings in the locale specific date-time format, using the locale of the database server. If there is an ambiguity, the built-in formats above take precedence.

Please see <span class="ItalicFont">[Working With Date and Time Values](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span> for information about using simple arithmetic with <span class="CodeFont">TIME</span> values.

Examples

``` Example
VALUES TIME('15:09:02');
VALUES '15:09:02';
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](../BuiltInFcns/CurrentDate.html) function
-   [<span class="CodeFont">DATE</span>](Date.html) data type
-   [<span class="CodeFont">DATE</span>](../BuiltInFcns/Date.html) function
-   [<span class="CodeFont">DAY</span>](../BuiltInFcns/Day.html) function
-   [<span class="CodeFont">EXTRACT</span>](../BuiltInFcns/Extract.html) function
-   [<span class="CodeFont">LASTDAY</span>](../BuiltInFcns/LastDay.html) function
-   [<span class="CodeFont">MONTH</span>](../BuiltInFcns/Month.html) function
-   [<span class="CodeFont">MONTH\_BETWEEN</span>](../BuiltInFcns/MonthBetween.html) function
-   [<span class="CodeFont">MONTHNAME</span>](../BuiltInFcns/MonthName.html) function
-   [<span class="CodeFont">NEXTDAY</span>](../BuiltInFcns/NextDay.html) function
-   [<span class="CodeFont">NOW</span>](../BuiltInFcns/Now.html) function
-   [<span class="CodeFont">QUARTER</span>](../BuiltInFcns/Quarter.html) function
-   [<span class="CodeFont">TIMESTAMP</span>](../BuiltInFcns/TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](../BuiltInFcns/ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](../BuiltInFcns/ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](../BuiltInFcns/Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


