[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Float.html)

<a href="" id="DataTypes.Float"></a>[]()FLOAT
=============================================

The <span class="CodeFont">FLOAT</span> data type is an alias for either a <span class="CodeFont">[REAL](Real.html)</span> or <span class="CodeFont">[DOUBLE PRECISION](DoublePrecision.html)</span> data type, depending on the precision you specify.

Syntax

``` FcnSyntax
FLOAT [ (precision) ]
```

precision

The default precision for <span class="CodeFont">FLOAT</span> is <span class="CodeFont">52</span>, which is equivalent to <span class="CodeFont">DOUBLE PRECISION</span>.

A precision of <span class="CodeFont">23</span> or less makes <span class="CodeFont">FLOAT</span> equivalent to <span class="CodeFont">REAL</span>.

A precision of <span class="CodeFont">24</span> or greater makes <span class="CodeFont">FLOAT</span> equivalent to <span class="CodeFont">DOUBLE PRECISION</span>.

If you specify a precision of <span class="CodeFont">0</span>, you get an error. If you specify a negative precision, you get a syntax error.

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
REAL or DOUBLE
```

Usage Notes

If you are using a precision of <span class="CodeFont">24</span> or greater, the limits of <span class="CodeFont">FLOAT</span> are similar to the limits of <span class="CodeFont">DOUBLE</span>.

If you are using a precision of <span class="CodeFont">23</span> or less, the limits of <span class="CodeFont">FLOAT</span> are similar to the limits of <span class="CodeFont">REAL</span>.

<span class="autonumber"><span class="noteAutoNum">RELEASE NOTE:  </span></span>Data defined with type <span class="CodeFont">[float](#)</span> is actually stored in the database as type <span class="CodeFont">[double](Double.html)</span> at this time. Note that this does not cause a loss of precision, though the data may require slightly more space.

 


