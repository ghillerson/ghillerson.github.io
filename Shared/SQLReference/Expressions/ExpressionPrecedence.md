[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/ExpressionPrecedence.html)

<a href="" id="Expressions.ExpressionPrecedence"></a>Expression []()Precedence
==============================================================================

The precedence of operations from highest to lowest is:

-   <span class="CodeFont">(), ?,</span> Constant (including sign), <span class="CodeFont">NULL</span>, <span class="ItalicFont">ColumnReference</span>, <span class="ItalicFont">ScalarSubquery</span>, <span class="CodeFont">CAST</span>
-   <span class="CodeFont">LENGTH, CURRENT\_DATE, CURRENT\_TIME, CURRENT\_TIMESTAMP</span>, and other built-ins
-   unary <span class="CodeFont">+</span> and <span class="CodeFont">-</span>
-   <span class="CodeFont">\*, /, ||</span> (concatenation)
-   binary <span class="CodeFont">+</span> and <span class="CodeFont">-</span>
-   comparisons, quantified comparisons, <span class="CodeFont">EXISTS, IN, IS NULL, LIKE, BETWEEN, IS</span>
-   <span class="CodeFont">NOT</span>
-   <span class="CodeFont">AND</span>
-   <span class="CodeFont">OR</span>

You can explicitly specify precedence by placing expressions within parentheses. An expression within parentheses is evaluated before any operations outside the parentheses are applied to it.

Example

``` Example
(3+4)*9
(age < 16 OR age > 65) AND employed = TRUE
```

 


