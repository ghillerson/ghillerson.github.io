[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Date.html)

<a href="" id="DataTypes.Date"></a>[]()DATE
===========================================

The <span class="CodeFont">DATE</span> data type provides for storage of a year-month-day in the range supported by <span class="ItalicFont">java.sql.Date</span>.

Syntax

``` FcnSyntax
DATE
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.sql.Date
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
DATE
```

Usage Notes

Here are several notes about using the <span class="CodeFont">DATE</span> data type:

-   Dates, [times](Time.html), and [timestamps](TimeStamp.html) must not be mixed with one another in expressions.
-   Any value that is recognized by the <span class="ItalicFont">java.sql.Date</span> method is permitted in a column of the corresponding SQL date/time data type. Splice Machine supports the following formats for <span class="CodeFont">DATE</span>:
    ``` FcnSyntax
    yyyy-mm-dd
    mm/dd/yyyy
    dd.mm.yyyy
    ```

-   The first of the three formats above is the <span class="ItalicFont">java.sql.Date</span> format.
-   The year must always be expressed with four digits, while months and days may have either one or two digits.
-   Splice Machine also accepts strings in the locale specific date-time format, using the locale of the database server. If there is an ambiguity, the built-in formats above take precedence.

Please see <span class="ItalicFont">[Working With Date and Time Values](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span> for information about using simple arithmetic with <span class="CodeFont">DATE</span> values.

Examples

``` Example
VALUES DATE('1994-02-23');
VALUES '1993-09-01';
```

See Also

-   [<span class="CodeFont">CURRENT\_DATE</span>](../BuiltInFcns/CurrentDate.html) function
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
-   [<span class="CodeFont">TIME</span>](Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](../BuiltInFcns/TimeStamp.html) function
-   [<span class="CodeFont">TO\_CHAR</span>](../BuiltInFcns/ToChar.html) function
-   [<span class="CodeFont">TO\_DATE</span>](../BuiltInFcns/ToDate.html) function
-   [<span class="CodeFont">WEEK</span>](../BuiltInFcns/Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


