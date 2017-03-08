[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Concatenation.html)

<a href="" id="BuiltInFcns.Concatenation"></a>[]()Concatenation Operator
========================================================================

The concatenation operator, <span class="CodeFont">||</span>, concatenates its right operand onto the end of its left operand; it operates on character string or bit string expressions.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Since all built-in data types are implicitly converted to strings, this function can act on all built-in data types.

Syntax

``` FcnSyntax
{
   { CharacterExpression || CharacterExpression } |
   { BitExpression || BitExpression }
}
```

CharacterExpression

An expression.

expression1

An expression.

expressionN

You can specify more than two argument; you MUST specify at least two arguments.

Results

For character strings:

-   If both the left and right operands are of type <span class="CodeFont">[CHAR](../DataTypes/Char.html)</span>, the resulting type is <span class="CodeFont">CHAR</span>; otherwise, it is <span class="CodeFont">[VARCHAR](../DataTypes/Varchar.html)</span>.
-   The normal blank padding/trimming rules for <span class="CodeFont">CHAR</span> and <span class="CodeFont">VARCHAR</span> apply to the result of this operator.
-   The length of the resulting string is the sum of the lengths of both operands.

Examples

``` Example
   -- returns 'San Francisco Giants' 
splice> VALUES 'San' || ' ' || 'Francisco' || ' ' || 'Giants';

   -- returns NULL
splice> VALUES CAST (null AS VARCHAR(7))|| 'Something';

   -- returns 'Today it is: 93'
splice> VALUES 'Today it is: ' || '93';
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LENGTH</span>](Length.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


