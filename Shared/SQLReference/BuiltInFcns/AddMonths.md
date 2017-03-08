[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/AddMonths.html)

[]()ADD\_MONTHS
===============

The <span class="CodeFont">ADD\_MONTHS</span> function returns the date resulting from adding a number of months added to a specified date.

Syntax

``` FcnSyntax
ADD_MONTHS(Date source, int numOfMonths);
```

source

The source date. This can be a <span class="CodeFont">DATE</span> value, or any value that can be implicitly converted to <span class="CodeFont">DATE</span>.

numOfMonths

An integer value that specifies the number of months to add to the source date.

Results

The returned string always has data type <span class="CodeFont">DATE</span>.

If date is the last day of the month or if the resulting month has fewer days than the day component of date, then the result is the last day of the resulting month. Otherwise, the result has the same day component as date.

Examples

``` Example
splice> VALUES(ADD_MONTHS(CURRENT_DATE,5));
1 
----------
2015-02-22
1 row selected

splice> VALUES(ADD_MONTHS(CURRENT_DATE,-5));
1 
----------
2014-04-22
1 row selected

splice> VALUES(ADD_MONTHS(DATE(CURRENT_TIMESTAMP),-5));
1 
----------
2014-04-22
1 row selected

splice> VALUES(ADD_MONTHS(DATE('2014-01-31'),1));
1 
----------
2014-02-28
1 row selected
```

 


