[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Integer.html)

<a href="" id="BuiltInFcns.Integer"></a>[]()INTEGER
===================================================

The <span class="CodeFont">INTEGER</span> function returns an integer representation of a number or character string in the form of an integer constant.

Syntax

``` FcnSyntax
INT[EGER] (NumericExpression | CharacterExpression ) 
```

NumericExpression

An expression that returns a value of any built-in numeric data type.

CharacterExpression

An expression that returns a character string value of length not greater than the maximum length of a character constant. Leading and trailing blanks are eliminated and the resulting string must conform to the rules for forming an SQL integer constant. The character string cannot be a long string.

Results

The result of the function is a large integer.

-   If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.
-   If the argument is a numeric-expression, the result is the same number that would occur if the argument were assigned to a large integer column or variable. If the whole part of the argument is not within the range of integers, an error occurs. The decimal part of the argument is truncated if present.
-   If the argument is a character-expression, the result is the same number that would occur if the corresponding integer constant were assigned to a large integer column or variable.

Example

The following query truncates the number of innings pitches by using the <span class="CodeFont">INTEGER</span> function:

``` Example
splice> SELECT DisplayName, INTEGER(Innings) "Innings" 
   FROM Pitching JOIN Players ON Pitching.ID=Players.ID 
   WHERE Innings > 50 
   ORDER BY Innings DESC;
DISPLAYNAME             |Innings    
------------------------------------
Marcus Bamburger        |218        
Jason Larrimore         |218        
Milt Warrimore          |181        
Carl Marin              |179        
Charles Heillman        |177        
Larry Lintos            |175        
Randy Varner            |135        
James Grasser           |129        
Thomas Hillman          |123        
Jack Peepers            |110        
Tam Lassiter            |76         
Yuri Piamam             |76         
Ken Straiter            |74         
Gary Kosovo             |73         
Tom Rather              |68         
Steve Mossely           |63         
Carl Vanamos            |61         
Martin Cassman          |60         
Tim Lentleson           |60         
Sam Castleman           |58         
Steve Raster            |57         
Mitch Lovell            |55         
Harold Sermer           |51         

23 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)

 


