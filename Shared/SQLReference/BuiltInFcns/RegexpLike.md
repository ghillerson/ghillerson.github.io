[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/RegexpLike.html)

[]()REGEXP\_LIKE Operator
=========================

The <span class="CodeFont">REGEXP\_LIKE</span> operator returns <span class="CodeFont">true</span> if the string matches the regular expression. This function is similar to the <span class="CodeFont">LIKE</span> predicate, except that it uses regular expressions rather than simple wildcard character matching.

Syntax

``` FcnSyntax
REGEXP_LIKE( sourceString, patternString )
}
```

sourceString

The character expression to match against the regular expression.

patternString

The regular expression string used to search for a match in <span class="CodeItalicFont">sourceString</span>.

The pattern is a <span class="CodeFont">java.util.regex</span> pattern. You can find documentation for the JDK 8 version here: <http://docs.oracle.com/javase/8/docs/api/java/util/regex/package-summary.html>.

Results

Returns true if the <span class="CodeItalicFont">sourcestring</span> you are testing matches the specified regular expression in <span class="CodeItalicFont">patternString</span>.

Examples

The following query finds all players whose name begins with <span class="ItalicFont">Ste</span>:

``` Example
splice> SELECT DisplayName
   FROM Players
   WHERE REGEXP_LIKE(DisplayName, '^Ste.*');

DISPLAYNAME             
------------------------
Steve Raster            
Steve Mossely           
Stephen Tuvesco         

3 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   <span class="CodeFont">[CONCATENATION](Concatenation.html)</span> operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LENGTH</span>](Length.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


