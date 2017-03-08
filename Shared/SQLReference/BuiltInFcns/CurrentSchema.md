[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentSchema.html)

<a href="" id="BuiltInFcns.CurrentSchema"></a>[]()CURRENT SCHEMA
================================================================

<span class="CodeFont">CURRENT SCHEMA</span> returns the schema name used to qualify unqualified database object references.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">CURRENT SCHEMA</span> and <span class="CodeFont">CURRENT SQLID</span> are synonyms.

Syntax

``` FcnSyntax
CURRENT SCHEMA
```

-- or, alternatively:

``` FcnSyntax
CURRENT SQLID
```

Results

The returned value is a string with a length of up to 128 characters.

Examples

``` Example
   
splice> VALUES(CURRENT SCHEMA);
1
-------------------------------------------------------
SPLICE

1 row selected
```

 


