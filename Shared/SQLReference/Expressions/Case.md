[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/Case.html)

<a href="" id="Expressions.Case"></a>[]()CASE Expression
========================================================

The <span class="CodeFont">CASE</span> expression can be used for conditional expressions in Splice Machine.

Syntax

You can place a <span class="CodeFont">CASE</span> expression anywhere an expression is allowed. It chooses an expression to evaluate based on a boolean test.

``` FcnSyntax
CASE 
  WHEN booleanExpression THEN thenExpression 
  [ WHEN booleanExpression
    THEN thenExpression ]...  
    ELSE elseExpression 
END
```

<span class="ItalicFont">thenExpression</span> and <span class="ItalicFont">elseExpression</span>

Both are both that must be type-compatible. For built-in types, this means that the types must be the same or a built-in broadening conversion must exist between the types.

Example

``` Example
   -- returns 3
 CASE WHEN 1=1 THEN 3 ELSE 4 END;
 
  -- returns 7
 CASE
   WHEN 1 = 2 THEN 3
   WHEN 4 = 5 THEN 6
   ELSE 7
 END;
```

 


