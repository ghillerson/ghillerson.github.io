[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/BigInt.html)

<a href="" id="BuiltInFcns.BigInt"></a>[]()BIGINT
=================================================

The <span class="CodeFont">BIGINT</span> function returns a 64-bit integer representation of a number or character string in the form of an integer constant.

Syntax
------

``` FcnSyntax
BIGINT (CharacterExpression | NumericExpression ) 
```

CharacterExpression

An expression that returns a character string value of length not greater than the maximum length of a character constant. Leading and trailing blanks are eliminated and the resulting string must conform to the rules for forming an SQL integer constant. The character string cannot be a long string. If the argument is a CharacterExpression, the result is the same number that would occur if the corresponding integer constant were assigned to a big integer column or variable.

NumericExpression

An expression that returns a value of any built-in numeric data type. If the argument is a NumericExpression, the result is the same number that would occur if the argument were assigned to a big integer column or variable. If the whole part of the argument is not within the range of integers, an error occurs. The decimal part of the argument is truncated if present.

Results

The result of the function is a big integer.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span> value.

Example

Using the <span class="CodeFont">Batting</span> table from our Doc Examples database, select the <span class="CodeFont">TotalBases</span> column in big integer form for further processing in the application:

``` Example
splice> SELECT ID, BIGINT(TotalBases) "TotalBases" 
   FROM Batting 
   WHERE ID < 11;
ID    |TotalBases          
---------------------------
1     |262                 
2     |235                 
3     |174                 
4     |234                 
5     |245                 
6     |135                 
7     |170                 
8     |99                  
9     |135                 
10    |85                  

10 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html) data type

 


