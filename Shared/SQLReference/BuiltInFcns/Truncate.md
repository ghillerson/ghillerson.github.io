[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Truncate.html)

[]()TRUNC or TRUNCATE
=====================

This topic describes the <span class="CodeFont">TRUNCATE</span> built-in function, which you can use to truncate numeric, date, and timestamp values. You can use the abbreviation <span class="CodeFont">TRUNC</span> interchangeably with the full name, <span class="CodeFont">TRUNCATE</span>.

Syntax

``` FcnSyntax
TRUNCATE( number    [, numPlaces]  |
          date      [, truncPoint] |
          timestamp [, truncPoint] );
```

number

An integer or decimal number to be truncated.

date

A [<span class="CodeFont">DATE</span>](../DataTypes/Date.html) value to be truncated.

timestamp

A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value to be truncated.

numPlaces

An optional integer value that specifies the number of digits to truncate (made zero) when applying this function to a <span class="ItalicFont">number</span>.

-   If this value is positive, that many of the least significant digits (to the right of the decimal point) are truncated: <span class="CodeFont">truncate(123.456,2)</span> returns <span class="CodeFont">123.450</span>.
-   If this value is negative, that many of the least significant digits to the left of the decimal point are truncated: <span class="CodeFont">truncate(123.456,-1)</span> returns <span class="CodeFont">120.000</span>.
-   If this value is zero, the decimal portion of the number is truncated: <span class="CodeFont">truncate(123.456,0)</span> returns <span class="CodeFont">123.000</span>.
-   If this value is not specified, the decimal portion of the number is zero'ed, which means that <span class="CodeFont">truncate(123.456)</span> returns <span class="CodeFont">123.000</span>.

See the [Truncating Numbers](#Truncati) examples below.

truncPoint

An optional string that specifies the point at which to truncate (zero) a date or timestamp value. This can be one of the following values:

<span class="CodeFont">YEAR</span> or <span class="CodeFont">YR</span>

The year value is retained; other values are set to their minimum values.

<span class="CodeFont">MONTH</span> or <span class="CodeFont">MON</span> or <span class="CodeFont">MO</span>

The year and month values are retained; other values are set to their minimum values.

<span class="CodeFont">DAY</span>

The year, month, and day values are retained; other values are set to their minimum values.

<span class="CodeFont">HOUR </span>or <span class="CodeFont">HR</span>

The year, month, day, and hour values are retained; other values are set to their minimum values.

<span class="CodeFont">MINUTE </span>or <span class="CodeFont">MIN</span>

The year, month, day, hour, and minute values are retained; other values are set to their minimum values.

<span class="CodeFont">SECOND </span>or <span class="CodeFont">SEC</span>

The year, month, day, hour, minute, and second values are retained; the milliseconds value is set to <span class="CodeFont">0</span>.

<span class="CodeFont">MILLISECOND</span> or <span class="CodeFont">MILLI</span>

All of the values, including year, month, day, hour, minute, second, and milliseconds are retained.

The default value, if nothing is specified, is <span class="CodeFont">DAY</span>.

Examples

[]()Truncating Numbers

``` Example
splice> VALUES TRUNC(1234.456, 2);
1
----------------------
1234.450

splice> VALUES TRUNCATE(123.456,-1);
1
----------------------
120.000

splice> VALUES TRUNCATE(123.456,0);
1
----------------------
123.000

splice> VALUES TRUNCATE(123.456);
1
----------------------
123.000

splice> VALUES TRUNC(1234.456, 2);
1
----------------------
1234.450

splice> VALUES TRUNCATE(123.456,-1);
1
----------------------
120.000

splice> VALUES TRUNCATE(123.456,0);
1
----------------------
123.000
1 row selected

splice> VALUES TRUNCATE(123.456);
1
----------------------
123.000

VALUES TRUNCATE(1234.6789, 1);
-----------------------
12345.6000

VALUES TRUNCATE(12345.6789, 2);
-----------------------
12345.6700

VALUES TRUNCATE(12345.6789, -1);
-----------------------
12340.0000

VALUES TRUNCATE(12345.6789, 0);
-----------------------
12345.0000

VALUES TRUNCATE(12345.6789);
-----------------------
12345.0000
```

Truncating Dates

``` Example
VALUES TRUNCATE(DATE('1988-12-26'), 'year');
----------------------
1988-01-01

VALUES TRUNCATE(DATE('1988-12-26'), 'month');
----------------------
1988-12-01

VALUES TRUNCATE(DATE('1988-12-26'), 'day');
----------------------
1988-12-26

VALUES TRUNCATE(DATE('1988-12-26'));
----------------------
1988-12-26

VALUES TRUNCATE(DATE('2011-12-26'), 'MONTH');
----------------------
2011-12-01
```

Truncating Timestamps

``` Example
VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'year');
----------------------
2000-01-01 00:00:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'month');
----------------------
2000-06-01 00:00:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'day');
----------------------
2000-06-07 00:00:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'hour');
----------------------
2000-06-07 17:00:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'minute');
----------------------
2000-06-07 17:12:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'second');
----------------------
2000-06-07 17:12:30.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'), 'MONTH');
----------------------
2011-12-01 00:00:00.0

VALUES TRUNCATE(TIMESTAMP('2000-06-07 17:12:30.0'));
----------------------
2011-12-26 00:00:00.0
```

 


