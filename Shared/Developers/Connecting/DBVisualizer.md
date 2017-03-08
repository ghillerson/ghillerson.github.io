[Open topic with navigation](../../../index.html#Shared/Developers/Connecting/DBVisualizer.html)

[]()Connecting DbVisualizer with JDBC
=====================================

This topic describes how to connect the <span class="ItalicFont">DbVisualizer</span> database visualization tool to Splice Machine via <span class="ItalicFont">JDBC</span>, in these three steps:

1.  [Download DbVisualizer](#Download)
2.  [Set up the Splice Machine driver](#Set)
3.  [Create a connection between DbVisualizer and Splice Machine](#Create)

[]()Download DbVisualizer
-------------------------

You can download a free version of <span class="ItalicFont">DbVisualizer</span> from <http://www.dbvis.com>; make sure that you have the latest version. After downloading, install the product on your computer, which provides excellent installation help if you encounter any difficulties.

[]()Set up the Splice Machine Driver
------------------------------------

Follow the steps to create and configure the Splice Machine driver:

1.  Start DbVisualizer
2.  Select <span class="AppFontCustCode">Tools | Driver Manager</span> from DbVisualizer's top menu.
3.  Create a new driver in DbVisualizer:

    1.  Click the first icon at the top (the plus sign) to configure a new driver.
    2.  Enter the following values in the Driver Settings section to use our JDBC driver.

        <span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>You <span class="BoldFont">must</span> use the <span class="ItalicFont">Splice Machine</span> JDBC driver; other drivers will not work correctly.

        |               |                                                         |
        |---------------|---------------------------------------------------------|
        | Name:         | Splice Machine                                          |
        | URL Format:   | jdbc:splice://&lt;server&gt;:&lt;port:1527&gt;/splicedb |
        | Driver Class: | com.splicemachine.db.jdbc.ClientDriver                  |

        <img src="../../../Resources/Images/DbVisDriver1.jpg" class="indented" />

[]()Create a Connection
-----------------------

Follow the steps in this section to create a connection and start using DbVisualizer with Splice Machine. See the [DbVisualizer User's Guide](http://confluence.dbvis.com/display/HOME/Documentation+Home) for complete information about creating connections.

1.  If you've not already done so, start DbVisualizer
2.  Start the New Connection wizard:

    Start the connection wizard by clicking <span class="AppCommand">Create Database Connection</span> in the <span class="ItalicFont">Database</span> menu.

    Click the <span class="AppCommand">Use Wizard</span> button.

3.  Name your connection:

    Enter a name for the connection on the first Wizard page. For example, you might name it <span class="ItalicFont">Splice Machine Connection</span>.

    Click the <span class="AppCommand">Next</span> button in the Wizard.

4.  Select the driver:

    Select <span class="AppCommand">Splice Machine</span> as the Database Driver.

    Then click the <span class="AppCommand">Next</span> button again.

5.  Set up the connection:

    Fill in the fields in the connection wizard screen using these values:

    |                    |                                               |
    |--------------------|-----------------------------------------------|
    | Database URL:      | &lt;your Splice Machine database URL&gt;      |
    | Database Userid:   | &lt;your Splice Machine database user ID&gt;  |
    | Database Password: | &lt;your Splice Machine database password&gt; |

    <img src="../../../Resources/Images/DbVisWiz1.jpg" class="indented" />

6.  Click the <span class="AppCommand">Ping Server</span> button to verify that your connection can be established.

    Splice Machine must be running for the connection to be successful.

7.  Click the <span class="AppCommand">Finish</span> button to create the connection.

8.  Optionally set additional settings:

    You may want to configure some additional settings. For example, to control the timeout duration, use these steps:

    1.  Select Tools | Tools Properties from the top DBVisualizer menu.
    2.  Select Generic | Connection Keep-Alive from the Database tab.
    3.  Enter values for your connection.

        ![](../../../Resources/Images/DbVisToolProps.jpg)

Your connection is now listed in the left panel under <span class="AppCommand">Connections</span>. You can use it to explore the database schema, enter queries, and take advantage of all of the capabilities of <span class="ItalicFont">DBVisualizer</span>.

<span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>DbVisualizer's <span class="ItalicFont">SQL Commander</span> menu includes an option to <span class="ItalicFont">Strip Comments when Executing</span>. If you enable this option, any Splice Machine query hints that you use will be stripped out and won't be applied.

 


