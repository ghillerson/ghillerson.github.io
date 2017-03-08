[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Coalesce.html)

<a href="" id="BuiltInFcns.Coalesce"></a>[]()COALESCE
=====================================================

The <span class="CodeFont">COALESCE</span> function returns the first non-<span class="CodeFont">NULL</span> expression from a list of expressions.

You can also use <span class="CodeFont">COALESCE</span> as a variety of a <span class="CodeFont">CASE</span> expression. For example:

``` Example
COALESCE( expresssion_1, expression_2,...expression_n);
```

is equivalent to:

``` Example
CASE WHEN expression_1 IS NOT NULL THEN expression_1
   ELSE WHEN expression_1 IS NOT NULL THEN expression_2
 ...
   ELSE expression_n;
```

Syntax

``` FcnSyntax
COALESCE ( expression1, expression2 [, expressionN]* )
```

expression1

An expression.

expression1

An expression.

expressionN

You can specify more than two arguments; <span class="BoldFont">you MUST specify at least two arguments</span>.

Usage

<span class="CodeFont">VALUE</span> is a synonym for <span class="CodeFont">COALESCE</span> that is accepted by Splice Machine, but is not recognized by the SQL standard.

Results

The result is <span class="CodeFont">NULL</span> only if all of the arguments are <span class="CodeFont">NULL</span>.

An error occurs if all of the parameters of the function call are dynamic.

Example

``` Example
   -- create table with three different integer types
splice> SELECT ID, FldGames, PassedBalls, WildPitches, Pickoffs,
   COALESCE(PassedBalls, WildPitches, Pickoffs) as "FirstNonNull" 
   FROM Fielding 
   WHERE FldGames>50 
   ORDER BY ID;
ID    |FLDGA&|PASSE&|WILDP&|PICKO&|First&
-----------------------------------------
1     |142   |4     |20    |0     |4     
2     |131   |NULL  |NULL  |NULL  |NULL  
3     |99    |NULL  |NULL  |NULL  |NULL  
4     |140   |NULL  |NULL  |NULL  |NULL  
5     |142   |NULL  |NULL  |NULL  |NULL  
6     |88    |NULL  |NULL  |NULL  |NULL  
7     |124   |NULL  |NULL  |NULL  |NULL  
8     |51    |NULL  |NULL  |NULL  |NULL  
9     |93    |NULL  |NULL  |NULL  |NULL  
10    |79    |NULL  |NULL  |NULL  |NULL  
39    |73    |NULL  |NULL  |0     |0     
40    |52    |NULL  |NULL  |0     |0     
41    |70    |NULL  |NULL  |2     |2     
42    |55    |NULL  |NULL  |0     |0     
43    |77    |NULL  |NULL  |0     |0     
46    |67    |NULL  |NULL  |0     |0     
49    |134   |4     |34    |2     |4     
50    |119   |NULL  |NULL  |NULL  |NULL  
51    |147   |NULL  |NULL  |NULL  |NULL  
52    |148   |NULL  |NULL  |NULL  |NULL  
53    |152   |NULL  |NULL  |NULL  |NULL  
54    |64    |NULL  |NULL  |NULL  |NULL  
55    |93    |NULL  |NULL  |NULL  |NULL  
56    |147   |NULL  |NULL  |NULL  |NULL  
57    |85    |NULL  |NULL  |NULL  |NULL  
58    |62    |NULL  |NULL  |NULL  |NULL  
59    |64    |NULL  |NULL  |NULL  |NULL  
62    |53    |1     |11    |0     |1     
64    |59    |NULL  |NULL  |NULL  |NULL  
81    |76    |NULL  |NULL  |0     |0     
82    |71    |NULL  |NULL  |1     |1     
84    |68    |NULL  |NULL  |0     |0     
92    |81    |NULL  |NULL  |3     |3     

33 rows selected
```

 


