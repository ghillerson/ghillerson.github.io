[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Nullif.html)

<a href="" id="BuiltInFcns.Nullif"></a>[]()NULLIF
=================================================

The <span class="CodeFont">NULLIF</span> function compares the values of two expressions; if they are equal, it returns <span class="CodeFont">NULL</span>; otherwise, it returns the value of the first expression.

Syntax

``` FcnSyntax
NULLIF (expression1, expression2 )
```

expression1

The first .expression whose value you want to compare.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You cannot specify the literal <span class="CodeFont">NULL</span> for <span class="CodeItalicFont">expression1</span>.

expression2

The first .expression whose value you want to compare.

Results

The <span class="CodeFont">NULLIF</span> function is logically similar to the following [<span class="CodeFont">CASE</span>](../Expressions/Case.html) expression:

``` Example
CASE WHEN expression1 = expression2 THEN NULL ELSE expression1 END;
```

Example

``` Example
splice> Select DisplayName "Position Player", NULLIF(Position,'P') "Position"
   FROM Players 
   WHERE MOD(ID, 2)=1 
   ORDER BY Position;
Position Player         |Pos&
-----------------------------
Barry Morse             |1B  
David Janssen           |1B  
John Purser             |2B  
Kelly Tamlin            |2B  
Kelly Wacherman         |2B  
Mitch Duffer            |3B  
Mitch Canepa            |3B  
Buddy Painter           |C   
Andy Sussman            |C   
Yuri Milleton           |C   
Edward Erdman           |C   
Alex Paramour           |CF  
Pablo Bonjourno         |CF  
Jeremy Johnson          |CF  
Tad Philomen            |CF  
Nathan Nickels          |IF  
George Goomba           |IF  
Don Allison             |IF  
Trevor Imhof            |LF  
Elliot Andrews          |MI  
Greg Brown              |OF  
Jeremy Packman          |OF  
Jason Pratter           |OF  
Reed Lister             |OF  
Roger Green             |OF  
Charles Heillman        |NULL
Thomas Hillman          |NULL
Tam Lassiter            |NULL
Mitch Lovell            |NULL
Justin Oscar            |NULL
Gary Kosovo             |NULL
Steve Raster            |NULL
Jason Lilliput          |NULL
Cory Hammersmith        |NULL
Barry Bochner           |NULL
Carl Marin              |NULL
Larry Lintos            |NULL
Tim Lentleson           |NULL
Carl Vanamos            |NULL
Steve Mossely           |NULL
Manny Stolanaro         |NULL
Michael Hillson         |NULL
Neil Gaston             |NULL
Mo Grandosi             |NULL
Mark Hasty              |NULL
Stephen Tuvesco         |NULL
Joseph Arkman           |UT  

47 rows selected
```

See Also

-   [<span class="CodeFont">CASE</span>](../Expressions/Case.html) expression

 


