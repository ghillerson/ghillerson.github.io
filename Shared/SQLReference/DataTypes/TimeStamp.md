[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/TimeStamp.html)

<a href="" id="DataTypes.TimeStamp"></a>[]()TIMESTAMP
=====================================================

The <span class="CodeFont">TIMESTAMP</span> data type stores a combined <span class="CodeFont">[DATE](Date.html)</span> and <span class="CodeFont">[TIME](Time.html)</span> value that permits fractional seconds values of up to nine digits.

Syntax

``` FcnSyntax
TIMESTAMP
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.sql.Timestamp
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
TIMESTAMP
```

About Timestamp Formats

Splice Machine uses the following Java date and time pattern letters to construct timestamps:

| Pattern Letter | Description            | Format(s)                            |
|----------------|------------------------|--------------------------------------|
| y              | year                   | yy or yyyy                           |
| M              | month                  | MM                                   |
| d              | day in month           | dd                                   |
| h              | hour (0-12)            | hh                                   |
| H              | hour (0-23)            | HH                                   |
| m              | minute in hour         | mm                                   |
| s              | seconds                | ss                                   |
| S              | tenths of seconds      | SSS (up to 6 decimal digits: SSSSSS) |
| z              | time zone text         | e.g. Pacific Standard time           |
| Z              | time zone, time offset | e.g. -0800                           |

The default timestamp format for Splice Machine imports is: <span class="CodeFont">yyyy-MM-dd HH:mm:ss</span>, which uses a 24-hour clock, does not allow for decimal digits of seconds, and does not allow for time zone specification.

Please see <span class="ItalicFont">[Working With Date and Time Values](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span> for information about using simple arithmetic with <span class="CodeFont">TIMESTAMP</span> values.

### Examples

The following tables shows valid examples of timestamps and their corresponding format (parsing) patterns:

| Timestamp value             | Format Pattern           | Notes                                                                                                |
|-----------------------------|--------------------------|------------------------------------------------------------------------------------------------------|
| 2013-03-23 09:45:00         | yyyy-MM-dd HH:mm:ss      | This is the default pattern.                                                                         |
| 2013-03-23 19:45:00.98-05   | yyyy-MM-dd HH:mm:ss.SSZ  | This pattern allows up to 2 decimal digits of seconds, and requires a time zone specification.       |
| 2013-03-23 09:45:00-07      | yyyy-MM-dd HH:mm:ssZ     | This patterns requires a time zone specification, but does not allow for decimal digits of seconds.  |
| 2013-03-23 19:45:00.98-0530 | yyyy-MM-dd HH:mm:ss.SSZ  | This pattern allows up to 2 decimal digits of seconds, and requires a time zone specification.       |
| 2013-03-23 19:45:00.123     
                              
 2013-03-23 19:45:00.12       | yyyy-MM-dd HH:mm:ss.SSS  | This pattern allows up to 3 decimal digits of seconds, but does not allow a time zone specification. 
                                                                                                                                                                
                                                          Note that if your data specifies more than 3 decimal digits of seconds, an error occurs.              |
| 2013-03-23 19:45:00.1298    | yyyy-MM-dd HH:mm:ss.SSSS | This pattern allows up to 4 decimal digits of seconds, but does not allow a time zone specification. |

Usage Notes

Dates, times, and timestamps cannot be mixed with one another in expressions.

Splice Machine also accepts strings in the locale specific datetime format, using the locale of the database server. If there is an ambiguity, the built-in formats shown above take precedence.

<span class="autonumber"><span class="noteAutoNum">RELEASE NOTE:  </span></span>At this time,dates in <span class="CodeFont">[TimeStamp](#)</span> values only work correctly when limited to this range of date values:    <span class="CodeFont">1678-01-01 to 2261-12-31</span>

See Also

-   [About Data Types](Intro.NumericTypes.html)
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


