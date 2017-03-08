[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/UsingVTI.html)

[]()Using the Splice Machine Virtual Table Interface (VTI)[]()
==============================================================

The Virtual Table Interface (VTI) allows you to use an SQL interface with data that is external to your database. This topic introduces the Splice Machine VTI in these sections:

-   [About VTI](#About) describes the virtual table interface.
-   <a href="#Splice" class="MCXref xref">Splice Machine Built-in Virtual Table Interfaces</a> describes the virtual table interfaces built into Splice Machine, and provides examples of using each.
-   <a href="#Creating" class="MCXref xref">Creating a Custom Virtual Table Interface</a> walks you through the steps required to create a custom virtual table interface, and demonstrates how to simplify its use with a table function.
-   <a href="#VirtualFile" class="MCXref xref">The Splice Machine Built-in VTI Classes</a> provides reference descriptions of the virtual table interface classes built into by Splice Machine.

[]()About VTI
-------------

You can use the Splice Machine Virtual Table Interface (<span class="ItalicFont">VTI</span>) to access data in external files, libraries, and databases.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>A virtual table is a view of data stored elsewhere; the data itself is not duplicated in your Splice Machine database.

The external data source can be any information source, including:

-   XML formatted reports and logs.
-   Queries that run in external databases that support JDBC, such as Oracle and DB2.
-   RSS feeds.
-   Flat files in formats such as comma-separated value (csv) format.

### About Table Functions

A <span class="ItalicFont">table function</span> returns <span class="CodeFont">ResultSet</span> values that you can query like you do tables that live in your Splice Machine database. A table function is bound to a constructor for a custom VTI class. Here's an example of a declaration for a table function that is bound to the <span class="CodeFont">PropertiesFileVTI</span> class, which we walk you through implementing later in this topic:

``` Example
CREATE FUNCTION propertiesFile(propertyFilename VARCHAR(200))
    RETURNS TABLE
       (
         KEY_NAME varchar(100)
         VALUE varchar(200)
       )
    LANGUAGE JAVA
    PARAMETER STYLE SPLICE_JDBC_RESULT_SET
    READS SQL DATA
    EXTERNAL NAME 'com.splicemachine.tutorials.vti.PropertiesFIleVTI.getPropertiesFileVTI';
```

[]()Splice Machine Built-in Virtual Table Interfaces
----------------------------------------------------

Splice Machine provides two built-in VTI classes that you can use:

| Class         | Description                                                        | Implemented by                            |
|---------------|--------------------------------------------------------------------|-------------------------------------------|
| SpliceFileVTI | For querying delimited flat files, such as CSV files.              | com.splicemachine.derby.vti.SpliceFileVTI |
| SpliceJDBCVTI | For querying data from external sources that support the JDBC API. | com.splicemachine.derby.vti.SpliceJDBCVTI |

Each of these classes implements the <span class="CodeFont">DatasetProvider</span> interface, which is used by Spark for creating execution trees, and the <span class="CodeFont">VTICosting</span> interface, which is used by the Splice Machine optimizer.

#### SpliceFileVTI Example

For example, if we have an input file named <span class="CodeFont">vtiInfile.csv</span> that contains this information:

``` Example
sculligan,Relief Pitcher,27,08-27-2015,2015-08-27 08:08:08,06:08:08
jpeepers,Catcher,37,08-26-2015,2015-08-21 08:09:08,08:08:08
mbamburger,Manager,47,08-25-2015,2015-08-20 08:10:08,10:08:08
gbrown,Batting Coach,46,08-24-2015,2015-08-21 08:11:08,11:08:08
jardson,Left Fielder,34,08-23-2015,2015-08-22 08:12:08,11:08:08
```

We can use the <span class="CodeFont">SpliceFileVTI</span> class to select and display the contents of our input file:

``` Example
SELECT * FROM new com.splicemachine.derby.vti.SpliceFileVTI(
  '/<path>/data/vtiInfile.csv','',',') AS b
   (name VARCHAR(10), title VARCHAR(30), age INT, something VARCHAR(12), date_hired TIMESTAMP, clock TIME);

NAME        |TITLE             |AGE   |SOMETHING   |DATE_HIRED             |CLOCK
---------------------------------------------------------------------------------------
sculligan   |Relief Pitcher    |27    |08X-27-2015 |2015-08-27 08:08:08.0  |06:08:08
jpeepers    |Catcher           |37    |08-26-2015  |2015-08-21 08:09:08.0  |08:08:08
mbamburger  |Manager           |47    |08-25-2015  |2015-08-20 08:10:08.0  |10:08:08
gbrown      |Batting Coach     |46    |08-24-2015  |2015-08-21 08:11:08.0  |11:08:08
jardson     |Left Fielder      |34    |08-23X-2015 |2015-08-22 08:12:08.0  |11:08:08

5 rows selected
```

#### SpliceJDBCVTI Example

We can use the <span class="CodeFont">SpliceJDBCVTI</span> class to select and display the contents a table in a JDBC-compliant database. For example, here we query a table stored in a MySQL database:

``` Example
SELECT * FROM new com.splicemachine.derby.vti.SpliceJDBCVTI(
  'jdbc:mysql://localhost/hr?user=root&password=mysql-passwd','mySchema','myTable') AS b
   (name VARCHAR(10), title VARCHAR(30), age INT, something VARCHAR(12), date_hired TIMESTAMP, clock TIME);

NAME        |TITLE             |AGE   |SOMETHING   |DATE_HIRED             |CLOCK
---------------------------------------------------------------------------------------
sculligan   |Relief Pitcher    |27    |08X-27-2015 |2015-08-27 08:08:08.0  |06:08:08
jpeepers    |Catcher           |37    |08-26-2015  |2015-08-21 08:09:08.0  |08:08:08
mbamburger  |Manager           |47    |08-25-2015  |2015-08-20 08:10:08.0  |10:08:08
gbrown      |Batting Coach     |46    |08-24-2015  |2015-08-21 08:11:08.0  |11:08:08
jardson     |Left Fielder      |34    |08-23X-2015 |2015-08-22 08:12:08.0  |11:08:08

5 rows selected
```

[]()Creating a Custom Virtual Table Interface
---------------------------------------------

You can create a custom virtual table interface by creating a class that implements the <span class="CodeFont">DatasetProvider</span> and <span class="CodeFont">VTICosting</span> interfaces, which are described below.

You can then use your custom VTI within SQL queries by using VTI syntax, as shown in the examples in the previous section. You can also create a table function for your custom VTI, and then call that function in your queries, which simplifies using your interface.

This section walks you through creating a custom virtual table interface that reads and displays the property keys and values in a properties file. This interface can be executed using a table function or by specifying its full method name in SQL statements.

The full code for this example is in the Splice [Community Sample Code Repository on Github.](https://github.com/splicemachine/splice-community-sample-code)

The remainder of this section is divided into these subsections:

-   <a href="#Declare" class="MCXref xref">Declare Your Class</a>
-   <a href="#Implemen" class="MCXref xref">Implement the Constructors</a>
-   <a href="#Implemen2" class="MCXref xref">Implement Your Method to Generate Results</a>
-   <a href="#Implemen3" class="MCXref xref">Implement Costing Methods</a>
-   <a href="#Implemen4" class="MCXref xref">Implement Other DatasetProvider Methods</a>
-   <a href="#Use" class="MCXref xref">Use Your Custom Virtual Table Interface</a>

[]()Declare Your Class

The first thing you need to do is to declare your public class; since we're creating an interface to read property files, we'll call our class <span class="CodeFont">PropertiesFileVTI</span>. To create a custom VTI interface, you need to implement the following classes:

| Class           | Description                                                              |
|-----------------|--------------------------------------------------------------------------|
| DatasetProvider | Used by Spark to construct execution trees.                              |
| VTICosting      | Used by the Splice Machine optimizer to estimate the cost of operations. |

Here's the declaration:

``` Example
public class PropertiesFileVTI implements DatasetProvider, VTICosting {

    //Used for logging (and optional)
    private static final Logger LOG = Logger.getLogger(PropertiesFileVTI.class);

    //Instance variable that will store the name of the properties file that is being read
    private String fileName;

    //Provide external context which can be carried with the operation
    protected OperationContext operationContext;
```

[]()Implement the Constructors

This section describes the constructors that we implement for our custom class:

-   You need to implement an empty constructor if you want to use your class in table functions:

    ``` Example
    public PropertiesFileVTI()
    ```

-   This is the signature used by invoking the VTI using the class name in SQL queries:

    ``` Example
    public PropertiesFileVTI(String pfileName)
    ```

-   This static constructor is called by the VTI - Table Function.

    ``` Example
    public static DatasetProvider getPropertiesFileVTI(String fileName)
    ```

Here's our implementation of the constructors for the <span class="CodeFont">PropertiesFileVTI</span> class:

``` Example
public PropertiesFileVTI() {
}

public PropertiesFileVTI(String pfileName) {
    this.fileName = pfileName;
}

public static DatasetProvider getPropertiesFileVTI(String fileName) {
    return new PropertiesFileVTI(fileName);
}
```

[]()Implement Your Method to Generate Results

The heart of your virtual table interface is the <span class="CodeFont">DatasetProvider</span> method <span class="CodeFont">getDataSet</span>, which you override to generate and return a <span class="CodeFont">DataSet</span>. It's declaration looks like this:

``` Example
DataSet<LocatedRow> getDataSet(
        SpliceOperation op,       // References the op at the top of the stack
        DataSetProcessor dsp,     // Mechanism for constructing the execution tree
        ExecRow execRow ) throws StandardException;
```

The <span class="CodeFont">VTIOperation</span> process calls this method to compute the <span class="CodeFont">ResultSet</span> that it should return. Our <span class="CodeFont">PropertiesFileVTI</span> implementation is shown here:

``` Example
@Override
public DataSet<LocatedRow> getDataSet(SpliceOperation op, DataSetProcessor dsp, ExecRow execRow) throws StandardException {
    operationContext = dsp.createOperationContext(op);

        //Create an arraylist to store the key-value pairs
    ArrayList<LocatedRow> items = new ArrayList<LocatedRow>();

    try {
        Properties properties = new Properties();

        //Load the properties file
        properties.load(getClass().getClassLoader().getResourceAsStream(fileName));

        //Loop through the properties and create an array
        for (String key : properties.stringPropertyNames()) {
            String value = properties.getProperty(key);
            ValueRow valueRow = new ValueRow(2);
            valueRow.setColumn(1, new SQLVarchar(key));
            valueRow.setColumn(2, new SQLVarchar(value));
            items.add(new LocatedRow(valueRow));
        }
    } catch (FileNotFoundException e) {
        LOG.error("File not found: " + this.fileName, e);
    } catch (IOException e) {
        LOG.error("Unexpected IO Exception: " + this.fileName, e);
    } finally {
        operationContext.popScope();
    }
    return new ControlDataSet<>(items);
}
```

[]()Implement Costing Methods

The Splice Machine optimizer uses costing estimates to determine the optimal execution plan for each query. You need to implement several costing methods in your VTI class:

-   <span class="CodeFont">getEstimatedCostPerInstantiation</span> returns the estimated cost to instantiate and iterate through your table function. Unless you have an accurate means of estimating this cost, simply return <span class="CodeFont">0</span> in your implementation.

    ``` Example
    public double getEstimatedCostPerInstantiation( VTIEnvironment vtiEnv) throws SQLException;
    ```

-   <span class="CodeFont">getEstimatedRowCount</span> returns the estimated row count for a single scan of your table function. Unless you have an accurate means of estimating this cost, simply return <span class="CodeFont">0</span> in your implementation.

    ``` Example
    public double getEstimatedCostPerInstantiation( VTIEnvironment vtiEnv) throws SQLException;
    ```

-   <span class="CodeFont">supportsMultipleInstantiations</span> returns a Boolean value indicating whether your table function's <span class="CodeFont">ResultSet</span> can be instantiated multiple times in a single query. For our <span class="CodeFont">PropertiesFileVTI</span> implementation of this method, we simply return <span class="CodeFont">False</span>, since there's no reason for our function to be used that way.

    ``` Example
    public double supportsMultipleInstantiations( VTIEnvironment vtiEnv) throws SQLException;
    ```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The VTICosting methods each take a <span class="CodeFont">VTIEnvironment</span> argument; this is a state variable created by the Splice Machine optimizer, which methods can use to pass information to each other or to learn other details about the operating environment..

Here is the implementation of costing methods for our <span class="CodeFont">PropertiesFileVTI</span> class:

``` Example
@Override
public double getEstimatedCostPerInstantiation(VTIEnvironment arg0) throws SQLException {
    return 0;
}

@Override
public double getEstimatedRowCount(VTIEnvironment arg0) throws SQLException {
    return 0;
}


@Override
public boolean supportsMultipleInstantiations(VTIEnvironment arg0) throws SQLException {
    return false;
}
```

[]()Implement Other DatasetProvider Methods

You also need to implement two additional <span class="CodeFont">DatasetProvider</span> methods:

-   <span class="CodeFont">getOperationContext</span> simply returns the current operation context (this.<span class="CodeFont">operationContext</span>).

    ``` Example
    OperationContext getOperationContext();
    ```

-   <span class="CodeFont">getMetaData</span> returns metadata that is used to dynamically bind your table function; this metadata includes a column descriptor for each column in your virtual table, including the name of the column, its type, and its size. In our <span class="CodeFont">PropertiesFileVTI</span>, we assign the descriptors to a static variable, and our implementation of this method simply returns that value.

    ``` Example
    ResultSetMetaData getMetaData() throws SQLException;
    ```

Here is the implementation of these methods for our <span class="CodeFont">PropertiesFileVTI</span> class:

``` Example
@Override
public OperationContext getOperationContext() {
    return this.operationContext;
}

@Override
public ResultSetMetaData getMetaData() throws SQLException {
    return metadata;
}

private static final ResultColumnDescriptor[] columnInfo = {
        EmbedResultSetMetaData.getResultColumnDescriptor("KEY1", Types.VARCHAR, false, 200),
        EmbedResultSetMetaData.getResultColumnDescriptor("VALUE", Types.VARCHAR, false, 200),
};

private static final ResultSetMetaData metadata = new EmbedResultSetMetaData(columnInfo);
}
```

[]()Use Your Custom Virtual Table Interface

You can create a table function in your Splice Machine database to simplify use of your custom VTI. Here's a table declaration for our custom interface:

``` Example
CREATE FUNCTION propertiesFile(propertyFilename VARCHAR(200))
    RETURNS TABLE
       (
         KEY_NAME varchar(100)
         VALUE varchar(200)
       )
    LANGUAGE JAVA
    PARAMETER STYLE SPLICE_JDBC_RESULT_SET
    READS SQL DATA
    EXTERNAL NAME 'com.splicemachine.tutorials.vti.PropertiesFIleVTI.getPropertiesFileVTI';
```

You can now use your interface with table function syntax; for example:

``` Example
select * from table (propertiesFile('sample.properties')) b;
```

You can also use your interface by using VTI syntax in an SQL query; for example:

``` Example
select * from new com.splicemachine.tutorials.vti.PropertiesFileVTI('sample.properties') 
   as b (KEY_NAME VARCHAR(20), VALUE VARCHAR(100));
```

[]()The Splice Machine Built-in VTI Classes
-------------------------------------------

This section describes the built-in VTI classes:

-   [The <span class="CodeFont">SpliceFileVTI</span> class](#The)
-   [The <span class="CodeFont">SpliceJDBCVTI</span> class](#Using)

### []()The SpliceFileVTI Class

You can use the <span class="CodeFont">SpliceFileVTI</span> class to apply SQL queries to a file, such as a csv file, as shown in the examples below.

#### Constructors

You can use the following constructor methods with the <span class="CodeFont">SpliceFileVTI</span> class. Each creates a virtual table from a file:

``` FcnSyntax
public SpliceFileVTI(String fileName)
```

``` FcnSyntax
public SpliceFileVTI(String fileName,
                     String characterDelimiter,
                     String columnDelimiter)
```

``` FcnSyntax
public SpliceFileVTI(String fileName,
                     String characterDelimiter,
                     String columnDelimiter,
                     boolean oneLineRecords)
```

``` FcnSyntax
public SpliceFileVTI(String fileName,
                     String characterDelimiter,
                     String columnDelimiter,
                     int[] columnIndex)
```

``` FcnSyntax
public SpliceFileVTI(String fileName,
                     String characterDelimiter,
                     String columnDelimiter,
                     int[] columnIndex,
                     String timeFormat,
                     String dateTimeFormat,
                     String timeStampFormat)
```

``` FcnSyntax
public SpliceFileVTI(String fileName,
                     String characterDelimiter,
                     String columnDelimiter,
                     int[] columnIndex,
                     String timeFormat,
                     String dateTimeFormat,
                     String timeStampFormat,
                     String oneLineRecords,
                     String charset)
```

fileName

The name of the file that you are reading.

characterDelimiter

Specifies which character is used to delimit strings in the imported data. You can specify <span class="CodeFont">null</span> or the empty string (<span class="CodeFont">''</span>) to use the default string delimiter, which is the double-quote (<span class="CodeFont">"</span>). If your input contains control characters such as newline characters, make sure that those characters are embedded within delimited strings.

columnDelimiter

The character used to separate columns, Specify <span class="CodeFont">null</span> if using the comma (<span class="CodeFont">,</span>) character as your delimiter. Note that the backslash (<span class="CodeFont">\\</span>) character is not allowed as the column delimiter.

oneLineRecords (boolean version)

A Boolean value that specifies whether each line in the import file contains one complete record; if you specify false, records can span multiple lines in the input file.

oneLineRecords (String version)

The string representation of a Boolean value that specifies whether each line in the import file contains one complete record; if you specify false, records can span multiple lines in the input file. A case-insensitive value of <span class="CodeFont">"True"</span> is parsed to the Boolean value <span class="CodeFont">true</span>; anything else is parse as <span class="CodeFont">false</span>.

columnIndex

An array of integers, each of which represents the index of a column that you want to read from the input file. Specify <span class="CodeFont">null</span> to read all files.

timeFormat

The format of timeFormats stored in the file. You can set this to null if there are no time columns in the file, or if the format of any times in the file match pattern: "<span class="ItalicFont">hh:mm:ss</span>".

dateTimeFormat

The format of datestamps stored in the file. You can set this to <span class="CodeFont">null</span> if there are no date columns in the file, or if the format of any dates in the file match pattern: "<span class="ItalicFont">yyyy-mm-dd</span>".

timestampFormat

The format of timestamps stored in the file. You can set this to <span class="CodeFont">null</span> if there are no timestamps in the file, or if the format of any timestamps in the file match the <span class="CodeFont">Java.sql.Timestamp</span> default format, which is: "<span class="ItalicFont">yyyy-MM-dd HH:mm:ss</span>".

charset

The character encoding of the import file. The default value is UTF-8. Currently, any other value is ignored and UTF-8 is used.

### []()The SpliceJDBCVTI Class

You can use the <span class="CodeFont">SpliceJDBCVTI</span> class to access external databases that provide JDBC connections.

#### Constructors

You can use the following constructor methods with the <span class="CodeFont">SpliceJDBCVTI</span> class.

``` FcnSyntax
public SpliceJDBCVTI(String connectionUrl,
                     String schemaName,
                     String tableName)
```

connectionURL

The URL of the database connection you are using.

schemaName

The name of the database schema.

tableName

The name of the table in the database schema.

``` FcnSyntax
public SpliceJDBCVTI(String connectionUrl,
                     String sql)
```

connectionURL

The URL of the database connection you are using.

sql

The SQL string to execute in that database.

See Also

We recommend visiting the [Derby VTI documentation](http://db.apache.org/derby/docs/10.9/publishedapi/jdbc3/org/apache/derby/vti/package-summary.html), which provides full reference documentation for the VTI class hierarchy.

 


