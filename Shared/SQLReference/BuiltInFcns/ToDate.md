[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/ToDate.html)

[]()TO\_DATE
============

The <span class="CodeFont">TO\_DATE</span> function formats a date string according to a formatting specification, and returns a <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> value. Note that <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> values do not store time components.

Syntax

``` FcnSyntax
TO_DATE( dateStrExpr, formatStr );
```

dateStrExpr

A string expression that contains a date that is formatted according to the format string.

<span class="ItalicFont">formatStr</span>

A string that specifies the format you want applied to the <span class="CodeFont">dateStr</span>. See the [Date and Time Formats](#Date) section below for more information about format specification.

Results

The result is always a <span class="CodeFont">[DATE](../DataTypes/Date.html)</span> value.

[]()Date and Time Formats

Splice Machine supports date and time format specifications based on the Java [SimpleDateFormat](http://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html#rfc822timezone) class.

Date and time value formats are used for both parsing input values and for formatting output values. For example, the format specification <span class="CodeFont">yyyy-MM-dd HH:mm:ssZ</span> parses or formats values like <span class="CodeFont">2014-03-02 11:47:44-0800</span>.

The remainder of this topic describes format specifications in these sections:

-   [Pattern Specifications](#Pattern) contains a table showing details for all of the pattern letters you can use.
-   [Presentation Types](#Presenta) describes how certain pattern letters are interpreted for parsing and/or formatting.
-   [Examples](#Presenta) contains a number of examples that will help you understand how to use formats.

[]()Pattern Specifications

You can specify formatting or parsing patterns for date-time values using the pattern letters shown in the following table. Note that pattern letters are typically repeated in a format specification. For example, <span class="CodeFont">YYYY</span> or <span class="CodeFont">YY</span>. Refer to the next section for specific information about multiple pattern letters in the different [presentation types](#Presenta).

| Pattern Letter | Meaning                                                                          | Presentation Type  | Example                                                                                                   |
|----------------|----------------------------------------------------------------------------------|--------------------|-----------------------------------------------------------------------------------------------------------|
| G              | Era designator                                                                   | Text               | BC                                                                                                        |
| y              | Year                                                                             | Year               | 2015 <span class="bodyFont">-or-</span> 15                                                                |
| Y              | Week year                                                                        | Year               | 2011 <span class="bodyFont">-or-</span> 11                                                                |
| M              | Month in year                                                                    | Month              | July <span class="bodyFont">-or-</span> Jul <span class="bodyFont">-or-</span> 07                         |
| w              | Week in year                                                                     | Number             | 27                                                                                                        |
| W              | Week in month                                                                    | Number             | 3                                                                                                         |
| D              | Day in year                                                                      | Number             | 212                                                                                                       
                                                                                                                                                                                                                                     
                                                                                                                          A common usage error is to mistakenly specify <span class="CodeFont">DD</span> for the day field:          
                                                                                                                                                                                                                                     
                                                                                                                          -   use <span class="CodeFont">dd</span> to specify day of month                                           
                                                                                                                          -   use <span class="CodeFont">DD</span> to specify the day of the year                                    |
| d              | Day in month                                                                     | Number             | 13                                                                                                        |
| F              | Day of week in month                                                             | Number             | 2                                                                                                         |
| E              | Day name in week                                                                 | Text               | Tuesday <span class="bodyFont">-or-</span> Tue                                                            |
| u              | Day number of week                                                               
                  (<span class="CodeFont">1</span>=Monday, <span class="CodeFont">7</span>=Sunday)  | Number             | 4                                                                                                         |
| a              | AM / PM marker                                                                   | Text               | PM                                                                                                        |
| H              | Hour in day                                                                      
                  (<span class="CodeFont">0 - 23</span>)                                            | Number             | 23                                                                                                        |
| k              | Hour in day                                                                      
                  <span class="CodeFont">(1 - 24)</span>                                            | Number             | 24                                                                                                        |
| K              | Hour in AM/PM                                                                    
                  (<span class="CodeFont">0 - 11</span>)                                            | Number             | 11                                                                                                        |
| h              | Hour in AM/PM                                                                    
                  (<span class="CodeFont">1 - 12</span>)                                            | Number             | 12                                                                                                        |
| m              | Minute in hour                                                                   | Number             | 33                                                                                                        |
| s              | Second in minute                                                                 | Number             | 55                                                                                                        |
| S              | Millisecond                                                                      | Number             | 959                                                                                                       |
| z              | Time zone                                                                        | General time zone  | Pacific Standard Time <span class="bodyFont">-or-</span> PST <span class="bodyFont">-or-</span> GMT-08:00 |
| Z              | Time zone                                                                        | RFC 822 time zone  | -0800                                                                                                     |
| X              | Time zone                                                                        | ISO 8601 time zone | -08 <span class="bodyFont">-or-</span> -0800 <span class="bodyFont">-or-</span> -08:00                    |
| '              | Escape char for text                                                             | Delimiter          |                                                                                                           |
| ''             | Single quote                                                                     | Literal            | '                                                                                                         |

[]()Presentation Types

How a presentation type is interpreted for certain pattern letters depends on the number of repeated letters in the pattern. In some cases, as noted in the following table, other factors can influence how the pattern is interpreted.

| Presentation Type        | Description                                                                                                                                                                                                                                                                            |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Text                     | For formatting, if the number of pattern letters is 4 or more, the full form is used. Otherwise, a short or abbreviated form is used, if available.                                                                                                                                    
                                                                                                                                                                                                                                                                                                                    
                            For parsing, both forms are accepted, independent of the number of pattern letters.                                                                                                                                                                                                     |
| Number                   | For formatting, the number of pattern letters is the minimum number of digits, and shorter numbers are zero-padded to this amount.                                                                                                                                                     
                                                                                                                                                                                                                                                                                                                    
                            For parsing, the number of pattern letters is ignored unless it's needed to separate two adjacent fields.                                                                                                                                                                               |
| Year                     
 (for Gregorian calendar)  | For formatting, if the number of pattern letters is 2, the year is truncated to 2 digits; otherwise it is interpreted as a number.                                                                                                                                                     
                                                                                                                                                                                                                                                                                                                    
                            For parsing, if the number of pattern letters is more than 2, the year is interpreted literally, regardless of the number of digits; e.g.:                                                                                                                                              
                                                                                                                                                                                                                                                                                                                    
                            -   if you use the pattern <span class="CodeFont">MM/dd/yyyy</span>, the value <span class="CodeFont">01/11/12</span> parses to <span class="CodeFont">January 11, 12 A.D.</span>                                                                                                       
                            -   if you use the pattern <span class="CodeFont">MM/dd/yy</span>, the value <span class="CodeFont">01/11/12</span> parses to <span class="CodeFont">January 11, 2012.</span>                                                                                                           
                                                                                                                                                                                                                                                                                                                    
                            If the number of pattern letters is one or two, (<span class="CodeFont">y</span> or <span class="CodeFont">yy</span>), the abbreviated year is interpreted as relative to a century; this is done by adjusting dates to be within 80 years before and 20 years after the current date.  |
| Year                     
 (other calendar systems)  | Calendar-system specific forms are applied.                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                                                    
                            For both formatting and parsing, if the number of pattern letters is 4 or more, a calendar specific long form is used. Otherwise, a calendar specific short or abbreviated form is used.                                                                                                |
| Month                    | If the number of pattern letters is 3 or more, the month is interpreted as text; otherwise, it is interpreted as a number.                                                                                                                                                             |
| General time zone        | Time zones are interpreted as text if they have names.                                                                                                                                                                                                                                 
                                                                                                                                                                                                                                                                                                                    
                            For time zones representing a GMT offset value, the following syntax is used:                                                                                                                                                                                                           
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">GMT Sign Hours : Minutes </span>                                                                                                                                                                                                                                 
                                                                                                                                                                                                                                                                                                                    
                            where:                                                                                                                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">Sign</span> is <span class="CodeFont">+</span> or <span class="CodeFont">-</span>                                                                                                                                                                                
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">Hours</span> is either <span class="CodeFont">Digit</span> or <span class="CodeFont">Digit Digit</span>, between <span class="CodeFont">0</span> and <span class="CodeFont">23</span>.                                                                           
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">Minutes</span> is <span class="CodeFont">Digit Digit</span> and must be between <span class="CodeFont">00</span> and <span class="CodeFont">59</span>.                                                                                                           
                                                                                                                                                                                                                                                                                                                    
                            For parsing, RFC 822 time zones are also accepted.                                                                                                                                                                                                                                      |
| RFC 822 time zone        | For formatting, use the RFC 822 4-digit time zone format is used:                                                                                                                                                                                                                      
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">Sign TwoDigitHours Minutes</span>                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                                                    
                            <span class="CodeFont">TwoDigitHours</span> must be between <span class="CodeFont">00</span> and <span class="CodeFont">23</span>.                                                                                                                                                      
                                                                                                                                                                                                                                                                                                                    
                            For parsing General time zones are also accepted.                                                                                                                                                                                                                                       |
| ISO 8601 time zone       | The number of pattern letters designates the format for both formatting and parsing as follows:                                                                                                                                                                                        
                                                                                                                                                                                                                                                                                                                    
                            ```                                                                                                                                                                                                                                                                                     
                              Sign TwoDigitHours Z                                                                                                                                                                                                                                                                  
                            | Sign TwoDigitHours Minutes Z                                                                                                                                                                                                                                                          
                            | Sign TwoDigitHours : Minutes Z                                                                                                                                                                                                                                                        
                            ```                                                                                                                                                                                                                                                                                     
                                                                                                                                                                                                                                                                                                                    
                            For formatting:                                                                                                                                                                                                                                                                         
                                                                                                                                                                                                                                                                                                                    
                            -   if the offset value from GMT is 0, <span class="CodeFont">Z</span> value is produced                                                                                                                                                                                                
                            -   if the number of pattern letters is 1, any fraction of an hour is ignored                                                                                                                                                                                                           
                                                                                                                                                                                                                                                                                                                    
                            For parsing, Z is parsed as the UTC time zone designator. Note that General time zones <span class="ItalicFont">are not accepted</span>.                                                                                                                                                |
| Delimiter                | Use the single quote to escape characters in text strings.                                                                                                                                                                                                                             |
| Literal                  | You can include literals in your format specification by enclosing the character(s) in single quotes.                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                                                    
                            Note that you must escape single quotes to include them as literals, e.g. use <span class="CodeFont">''T''</span> to include the literal string <span class="CodeFont">'T'</span>.                                                                                                      |

[]()Formatting Examples

The following table contains a number of examples of date time formats:

| Date and Time Pattern          | Result                                                            |
|--------------------------------|-------------------------------------------------------------------|
| "yyyy.MM.dd G 'at' HH:mm:ss z" | <span class="Example">2001.07.04 AD at 12:08:56 PDT</span>        |
| "EEE, MMM d, ''yy"             | <span class="Example">Wed, Jul 4, '01</span>                      |
| "h:mm a"                       | <span class="Example">12:08 PM</span>                             |
| "hh 'o''clock' a, zzzz"        | <span class="Example">12 o'clock PM, Pacific Daylight Time</span> |
| "K:mm a, z"                    | <span class="Example">0:08 PM, PDT</span>                         |
| "yyyyy.MMMMM.dd GGG hh:mm aaa" | <span class="Example">02001.July.04 AD 12:08 PM</span>            |
| "EEE, d MMM yyyy HH:mm:ss Z"   | <span class="Example">Wed, 4 Jul 2001 12:08:56 -0700</span>       |
| "yyMMddHHmmssZ"                | <span class="Example">010704120856-0700</span>                    |
| "yyyy-MM-dd'T'HH:mm:ss.SSSZ"   | <span class="Example">2001-07-04T12:08:56.235-0700</span>         |
| "yyyy-MM-dd'T'HH:mm:ss.SSSXXX" | <span class="Example">2001-07-04T12:08:56.235-07:00</span>        |
| "YYYY-'W'ww-u"                 | <span class="Example">2001-W27-3</span>                           |

Examples of Using <span class="CodeFont">TO\_DATE</span>

Here are several simple examples:

``` Example
splice> VALUES TO_DATE('2015-01-01', 'YYYY-MM-dd');
1 
----------
2015-01-01
1 row selected

splice> VALUES TO_DATE('01-01-2015', 'MM-dd-YYYY');
1 
----------
2015-01-01
1 row selected

splice> VALUES (TO_DATE('01-01-2015', 'MM-dd-YYYY') + 30);
1 
----------
2015-01-31
1 

splice> VALUES (TO_DATE('2015-126', 'MM-DDD'));
1 
----------
2015-05-06
1 row selected

splice> VALUES (TO_DATE('2015-026', 'MM-DDD'));
1
----------
2015-01-26

splice> VALUES (TO_DATE('2015-26', 'MM-DD'));
1
----------
2015-01-26
1 row selected
```

And here is an example that shows two interesting aspects of using <span class="CodeFont">TO\_DATE</span>. In this example, the input includes the literal <span class="CodeFont">T</span>), which means that the format pattern must delimit that letter with single quotes. Since we're delimiting the entire pattern in single quotes, we then have to escape those marks and specify <span class="CodeFont">''T''</span> in our parsing pattern.

And because this example specifies a time zone (Z) in the parsing pattern but not in the input string, the timezone information is not preserved. In this case, that means that the parsed date is actually a day earlier than intended:

``` Example
splice> VALUES TO_DATE('2013-06-18T01:03:30.000Z','yyyy-MM-dd''T''HH:mm:ss.SSSZ');
1
----------
2013-06-17
```

The solution is to explicitly include the timezone for your locale in the input string:

``` Example
splice> VALUES TO_DATE('2013-06-18T01:03:30.000-08:00','yyyy-MM-dd''T''HH:mm:ss.SSSZ');
1
----------
2013-06-18
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
-   [<span class="CodeFont">TO\_CHAR</span>](ToChar.html) function
-   [<span class="CodeFont">WEEK</span>](Week.html) function
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


