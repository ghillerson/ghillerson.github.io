[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/VarChar.html)

<a href="" id="BuiltInFcns.VarChar"></a>[]()VARCHAR
===================================================

The <span class="CodeFont">VARCHAR</span> function returns a varying-length character string representation of a character string.

Character to varchar syntax

``` FcnSyntax
VARCHAR (CharacterStringExpression ) 
```

CharacterStringExpression

An expression whose value must be of a character-string data type with a maximum length of <span class="CodeFont">32,672</span> bytes.

Datetime to varchar syntax

``` FcnSyntax
VARCHAR (DatetimeExpression ) 
```

DatetimeExpression

An expression whose value must be of a date, time, or timestamp data type.

Example

The <span class="AppCommand">Position</span> column in our <span class="AppCommand">Players</span> table is defined as <span class="CodeFont">CHAR(2)</span>. The following query show hows to access positon values as <span class="CodeFont">VARCHAR</span>s:

``` Example
splice> SELECT VARCHAR(Position) 
   FROM Players 
   WHERE ID < 11;
1   
----
C   
1B  
2B  
SS  
3B  
LF  
CF  
RF  
OF  
RF  

10 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html) data type

 


