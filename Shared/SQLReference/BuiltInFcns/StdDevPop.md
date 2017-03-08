[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/StdDevPop.html)

[]()STDDEV\_POP
===============

The <span class="CodeFont">STDDEV\_POP()</span> function returns the population standard deviation of a set of numeric values.

It returns <span class="CodeFont">NULL</span> if no matching row is found.

Syntax

``` FcnSyntax
STDDEV_POP ( [ DISTINCT | ALL ] expression )
```

DISTINCT

If this qualifier is specified, duplicates are eliminated

ALL

If this qualifier is specified, all duplicates are retained. This is the default value.

expression

An expression that evaluates to a numeric data type: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), or [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html).

The expression can contain multiple column references or expressions, but it cannot contain another aggregate or subquery, and it must evaluate to an ANSI SQL numeric data type. This means that you can call methods that evaluate to ANSI SQL data types.

If an expression evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Results

This function returns a double-precision number.

If the input expression consists of a single value, the result of the function is <span class="CodeFont">NULL</span>, not <span class="CodeFont">0</span>.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default.The database owner can grant access to other users.

Example

The following example shows computing the average, population standard deviation, and sample standard deviation from our Salaries table:

``` Example
splice> SELECT AVG(Salary) as AvgSalary, STDDEV_POP(Salary) AS PopStdDev, STDDEV_SAMP(Salary) As SampStdDev FROM Salaries;
AVGSALARY           |POPSTDDEV             |SAMPSTDDEV            
------------------------------------------------------------------
2949737             |4694155.715951055     |4719325.63212163      

1 row selected
```

 


