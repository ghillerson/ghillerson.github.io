[Open topic with navigation](../../index.html#OnPremise/InstallingSpliceMachine/Authentication.html)

Configuring Splice Machine Authentication
=========================================

This topic describes the mechanisms you can use in Splice Machine to authenticate users and how to configure the mechanism you choose to use, in these sections:

-   [Supported Authentication Mechanisms](#Supporte)
-   [Configuring Authentication](#Configur)

[]()Supported Authentication Mechanisms
---------------------------------------

You can use one of the following authentication mechanisms, each of which is described below the table:

| Authentication Mechanism | Description                                                                                                                                                                                                                           |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| None                     | Any user ID and password combination is allowed to connect to database.                                                                                                                                                               |
| Native                   | User IDs in a database table are validating against the corresponding, encrypted password.                                                                                                                                            
                                                                                                                                                                                                                                                                   
                            This is the default authentication setting for Splice Machine installations.                                                                                                                                                           |
| LDAP                     | User IDs are validating against an existing LDAP service.                                                                                                                                                                             
                                                                                                                                                                                                                                                                   
                            <span class="noteEnterpriseNote">ENTERPRISE ONLY: This feature is available only with a Splice Machine Enterprise license.</span>                                                                                                      
                                                                                                                                                                                                                                                                   
                            You cannot use this feature with the Community version of Splice Machine. For a list of the additional features available in the Enterprise edition, see our [Splice Machine Editions](../GettingStarted/SpliceEditions.html) page.    
                                                                                                                                                                                                                                                                   
                            To obtain a license for the Splice Machine <span class="ItalicFont">Enterprise Edition</span>, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>  |

[]()Configuring Authentication
------------------------------

You configure Splice Machine authentication by adding or updating properties in your HBase configuration file; this is typically done during installation of Splice Machine, but you can modify your settings whenever you want. This section contains the following subsections:

-   [Locating Your Configuration File](#Locating)
-   [Disabling Authentication](#Disablin)
-   [Using Native Authentication](#Using)
-   [Using LDAP Authentication](#Using2)

### []()Locating Your Configuration File

The following table specifies the platform-specific location of the configuration you need to update when changing your Splice Machine authentication properties:

| Platform           | Configuration file to modify with your authentication properties                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------|
| CDH                | <span class="PlatformVariablesCDH5AuthSettingsLoc">hbase-site.xml</span>                                                           |
| HDP                | <span class="PlatformVariablesHDP2AuthSettingsLoc">Select the Custom HBase Configs option from the HBase configuration tab.</span> |
| MapR               | <span class="PlatformVariablesMapRAuthSettingsLoc">hbase-site.xml</span>                                                           |
| Standalone version | <span class="PlatformVariablesStandaloneAuthSettingsLoc">splicemachine/lib/splice-site.xml</span>                                  |

Configure your authentication settings by adding or modifying properties in the configuration file.

### []()Disabling Authentication

If you want to disable authentication for your Splice Machine database, you can set the authentication property to <span class="CodeFont">NONE</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine <span class="BoldFont">strongly encourages you to not use</span> an open database for production databases!

You can configure an open database that allows any user to authenticate against the database by setting your authentication properties as follows:

``` ExampleCell
<property>
   <name>splice.authentication</name>
   <value>NONE</value>
</property>
```

### []()Using Native Authentication

Native authentication is the default mechanism for Splice Machine; you don't need to modify your configuration if you wish to use it. Native authentication uses the <span class="CodeFont">sys.sysusers</span> table in the <span class="CodeFont">splice</span> schema for configuring user names and passwords.

The default native authentication property settings are:

``` ExampleCell
<property>
   <name>splice.authentication</name>
   <value>NATIVE</value>
</property>
<property>
   <name>splice.authentication.native.algorithm</name>
   <value>SHA-512</value>
</property>
```

You can use <span class="CodeFont">MD5</span>, <span class="CodeFont">SHA-256</span>, or <span class="CodeFont">SHA-512</span> for the value of the <span class="HighlightedCode">native.algorithm</span> property; <span class="CodeFont">SHA-512</span> is the default value.

#### Switching to Native Authentication

If you are switching your authentication from to <span class="CodeFont">Native</span> authentication from another mechanism (including <span class="CodeFont">NONE</span>), there's one additional step you need to take: you must re-initialize the credentials database (<span class="CodeFont">SYSUSERS</span> table), by adding the following property setting to your configuration file:

``` Example
<property>
<name>splice.authentication.native.create.credentials.database</name>
<value>true</value>
</property>
```

### []()Using LDAP Authentication

LDAP authentication in Splice Machine uses an external LDAP server.

<span class="noteEnterpriseNote">ENTERPRISE ONLY: LDAP authentication is available only with a Splice Machine Enterprise license.</span>

You cannot use LDAP authentication with the Community version of Splice Machine.

To obtain a license for the Splice Machine Enterprise Edition, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](https://www.splicemachine.com/company/contact-us/) today.</span>

To use LDAP with Splice Machine, you must:

-   [Contact us](https://www.splicemachine.com/company/contact-us/) to obtain a license key from Splice Machine.
-   Enable Enterprise features by adding your Splice Machine license key to your HBase configuration file as the value of the <span class="CodeFont">splicemachine.enterprise.key</span> property, as shown below.
-   Make sure that a user with name <span class="CodeFont">splice</span> has been created in the LDAP server.
-   Add the Splice Machine LDAP properties in your HBase configuration file, along with the license key property:

#### LDAP Property Settings

These are the property settings you need to configure:

``` Example
<property>
   <name>splicemachine.enterprise.key</name>
   <value><your-Splice-Machine-license-key></value>
</property>
<property>
   <name>splice.authentication</name>
   <value>LDAP</value>
</property>
<property>
   <name>splice.authentication.ldap.server</name>
   <value><ldap://servername-ldap.yourcompany.com:389></value>
</property>
<property>
   <name>splice.authentication.ldap.searchAuthDN</name>
   <value><cn=commonName,ou=Users,dc=yourcompany,dc=com></value>
</property>
<property>
   <name>splice.authentication.ldap.searchAuthPW</name>
   <value><yourpassword</value>
</property>
<property>
   <name>splice.authentication.ldap.searchBase</name>
   <value>ou=Users,dc=yourcompany,dc=com</value>
</property>
<property>
   <name>splice.authentication.ldap.searchFilter</name>
   <value><(&amp;(objectClass=*)(uid=%USERNAME%))></value>
</property>
```

Notes about the LDAP property values:

-   Specify the location of your external LDAP server host in the <span class="Example">splice.authentication.ldap.server</span> property on port <span class="HighlightedCode">389</span>.
-   The <span class="HighlightedCode">ldap.searchAuthDN</span> property is the security principal:

    -   This is used to create the initial LDAP context (aka its connection to a specific DN).
    -   It must have the authority to search the user space for user DNs.
    -   The <span class="CodeFont">cn=</span> is the <span class="ItalicFont">common name</span> of the security principal.
-   The <span class="HighlightedCode">ldap.searchAuthPW</span> property specifies password Splice Machine should use to perform the DN search.
-   The <span class="HighlightedCode">ldap.searchBase</span> property specifies the root DN of the point in your hierarchy from which to begin a guest or anonymous search for the user's DN.
-   The <span class="HighlightedCode">ldap.searchFilter</span> property specifies the search filter to use to determine what constitutes a user while searching for a user DN

#### Connecting with JDBC and LDAP

You can then use our JDBC driver to connect to your database with LDAP authentication, using a connection string similar to this:

``` Example
jdbc:splice://localhost:1527/splicedb;user=yourName;password=yourPswd
```

 


