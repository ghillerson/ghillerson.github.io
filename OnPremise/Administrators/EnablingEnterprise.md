[Open topic with navigation](../../index.html#OnPremise/Administrators/EnablingEnterprise.html)

Enabling Enterprise Features in Splice Machine
==============================================

There are two mechanisms for enabling enterprise features in Splice Machine:

-   To access enterprise features such as Backup and Restore, you can simply call the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE](../../Shared/SQLReference/BuiltInSysProcs/EnableEnterprise.html)</span> built-in system procedure with the license key you obtain from Splice Machine, as described in the next section.
-   To unlock Splice Machine Enterprise features that require configuration changes in your HBase settings, such as Kerberos and LDAP, you need to add one or more properties to your configuration file, as described in [Using Configuration Properties to Upgrade to the Enterprise](#Using2), below.

[]()Using <span class="CodeFont">SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE</span> to Upgrade
----------------------------------------------------------------------------------------

If you want to use Enterprise features, such as Backup and Restore, that do not need system properties updated, you can call the <span class="CodeFont">SYSCS\_UTIL.SYSCS\_ENABLE\_ENTERPRISE</span> system procedure to unlock those features. You only need to do this once:

1.  Obtain your Splice Machine Enterprise Edition license key.
2.  Enter this command on the <span class="AppCommand">splice&gt;</span> command line:

    ``` AppCommandCell
    splice> CALL SYSCS_UTIL.SYSCS_ENABLE_ENTERPRISE('<yourLicenseKey>');
    Statement executed.
    ```

    If you enter an invalid license key, you'll see an error message:

    ``` AppCommandCell
    splice> CALL SYSCS_UTIL.SYSCS_ENABLE_ENTERPRISE ('<bogus-license>');
    Error
    -------------------------------
    ERROR XSRSE: Unable to enable the enterprise Manager. Enterprise services are disabled. Contact your Splice Machine representative to enable.
    ```

[]()Using Configuration Properties to Upgrade to the Enterprise
---------------------------------------------------------------

If your site uses Kerberos or LDAP, you need to update to the Enterprise version of Splice Machine by modifying your cluster's HBase configuration, and then restart Splice Machine. Follow these steps:

1.  Obtain your Splice Machine Enterprise Edition license key.
2.  Edit the <span class="CodeFont">hbase-site.xml</span> configuration file, adding this property:

    ``` Example
    <property>
       <name>splicemachine.enterprise.key</name>
       <value><your-Splice-Machine-license-key></value>
    </property>
    ```

3.  If you're using or switching from another authentication mechanism to LDAP, also add the LDAP properties to your <span class="CodeFont">hbase-site.xml</span> file, as described in the [Splice Machine Authentication and Authorization](../../Shared/Developers/Fundamentals/Authorization.html) topic.
4.  Restart Splice Machine, by first [Shutting DownYour Database](ShuttingDownDatabase.html), and then [Starting Your Database](StartingDatabase.html).

 


