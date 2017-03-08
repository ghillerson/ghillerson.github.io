[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/SmallInt.html)

<a href="" id="BuiltInFcns.SmallInt"></a>[]()SMALLINT
=====================================================

The <span class="CodeFont">SMALLINT</span> function returns a small integer representation of a number or character string, in the form of a small integer constant.

Syntax

``` FcnSyntax
SMALLINT ( NumericExpression | CharacterExpression )
```

NumericExpression

An expression that returns a value of any built-in numeric data type.

CharacterExpression

An expression that returns a character string value of length not greater than the maximum length of a character constant. Leading and trailing blanks are eliminated and the resulting string must conform to the rules for forming an SQL integer constant. The value of the constant must be in the range of small integers. The character string cannot be a long string.

Results

The result of the function is a [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html). If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>. If the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.

If the argument is a <span class="ItalicFont">NumericExpression</span>, the result is the same number that would occur if the argument were assigned to a small integer column or variable. If the whole part of the argument is not within the range of small integers, an error occurs. The decimal part of the argument is truncated if present.

If the argument is a <span class="ItalicFont">CharacterExpression</span>, the result is the same number that would occur if the corresponding integer constant were assigned to a small integer column or variable.

Examples

Using the <span class="CodeFont">Pitching</span> table from our Doc Examples database, select the <span class="CodeFont">Era</span> column in big integer form for further processing in the application:

``` Example
splice> SELECT ID, SMALLINT(Era) "ERA" 
   FROM Pitching 
   WHERE MOD(ID,2) = 0;
ID    |ERA   
-------------
28    |2     
30    |4     
32    |3     
34    |5     
36    |3     
38    |5     
40    |5     
42    |2     
44    |5     
46    |2     
48    |5     
72    |2     
74    |3     
76    |2     
78    |3     
80    |1     
82    |3     
84    |2     
86    |2     
88    |0     
90    |2     
92    |2     
94    |2     

23 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)

 


