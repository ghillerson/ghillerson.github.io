[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/EnableEnterprise.html)

<a href="" id="BuiltInSysProcs.EmptyStatementCache"></a>[]()SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE
=================================================================================================

The SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE stored procedure unlocks access to features that are only available in the Enterprise Edition of Splice Machine.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Calling SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE with a valid license key unlocks access to <span class="ItalicFont">Enterprise-only</span> features in Splice Machine such as backing up and restoring your database. However, to unlock bootstrapped authentication and encryption features such as LDAP and Kerberos, you must also modify your <span class="CodeFont">hbase-site.xml</span> file and restart Splice Machine.
Please see the [Upgrading to the Enterprise Edition of Splice Machine](../../../OnPremise/Administrators/EnablingEnterprise.html) topic in the <span class="ItalicFont">Administrator's Guide</span> for more information.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_ENABLE_ENTERPRISE( STRING license_key );
```

license\_key

The license key you received from Splice Machine.

SQL Example

``` Example
splice> CALL SYSCS_UTIL.SYSCS_ENABLE_ENTERPRISE (<your-license-code>);
Statement executed.
```

Results

This procedure does not return a result; however, if you provide an invalid license key, you'll see an error message displayed:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_ENABLE_ENTERPRISE (<bogus-code>);
Error
-------------------------------

ERROR XSRSE: Unable to enable the enterprise Manager. Enterprise services are disabled. Contact your Splice Machine representative to enable.
```

See Also

-   [Upgrading to the Enterprise Edition of Splice Machine](../../../OnPremise/Administrators/EnablingEnterprise.html) topic in the <span class="ItalicFont">Administrator's Guide</span>

 


