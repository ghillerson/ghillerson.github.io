[Open topic with navigation](../../../index.html#Shared/Developers/Connecting/Tableau.html)

[]()Connecting Tableau with ODBC
================================

This topic presents an example of connecting the <span class="ItalicFont">Tableau</span> business intelligence tool to Splice Machine via ODBC, and serves as an example of connecting other tools to Splice Machine with ODBC. This page describes connecting Tableau to Splice Machine on a Windows PC.

Follow these four steps to install and use a free trial version of <span class="ItalicFont">Tableau</span>.

1.  Install Tableau:

    Download <span class="ItalicFont">Tableau</span> from [www.tableausoftware.com](http://www.tableausoftware.com) and install it on your Windows system.

2.  Install and Configure the ODBC driver:

    Follow the instructions in our [ODBC Driver](ODBCDriver.html) topic to download, install, and configure our ODBC driver for your Windows or Linux computer.

    <span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>You <span class="BoldFont">must</span> use the <span class="ItalicFont">Splice Machine</span> ODBC driver; other drivers will not work correctly.

3.  Connect from Tableau:

    Now that you've got your data source set up, you can use it with Tableau. Follow these steps to connect to your data source in Tableau:

    1.  Open the list of connections:

        Click <span class="AppCommand">Connect to Data</span> on Tableau's opening screen to reveal the list of possible data connections.

    2.  Select ODBC:

        Scroll to the bottom of the <span class="AppCommand">On a server</span> list, and click <span class="AppCommand">Other Databases (ODBC)</span>.

    3.  Select your DSN and connect:

        Select the DSN you just created from the drop-down list, and then click the <span class="AppCommand">Connect</span> button.

    4.  Select the schema:

        Select the schema you want to work with (<span class="CodeFont">splice</span>), and then select the <span class="AppCommand">Single Table</span> option.

    5.  Select the table to view:

        Click the search (magnifying glass) icon, and then select the table you want to view from the drop-down list.

        For example, we choose the <span class="AppCommand">CUSTOMERS</span> table and specify <span class="AppCommand">CUSTOMERS (SPLICE)</span> as the connection name for use in Tableau.

    After you click <span class="AppCommand">OK</span>, <span class="ItalicFont">Tableau</span> is ready to work with your data.

 


