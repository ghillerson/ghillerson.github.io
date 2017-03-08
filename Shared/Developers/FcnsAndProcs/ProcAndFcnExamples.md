[Open topic with navigation](../../../index.html#Shared/Developers/FcnsAndProcs/ProcAndFcnExamples.html)

Examples of Splice Machine Functions and Stored Procedures
==========================================================

This topic walks you through creating, storing, and using a sample database function and a sample database stored procedure, in these sections:

-   [Creating and Using a Sample Function in Splice Machine](#CreatingSampleFunction)
-   [Creating and Using a Sample Stored Procedure in Splice Machine](#CreatingSampleProc)

[]()Creating and Using a Sample Function in Splice Machine
----------------------------------------------------------

This section walks you through creating a sample function named <span class="CodeFont">word\_limiter</span> that limits the number of words in a string; for example, given this sentence:

> <span class="AppCommand">Today is a wonderful day and I am looking forward to going to the beach.</span>

If you tell <span class="CodeFont">word\_limiter</span> to return the first five words in the sentence, the returned string would be:

> <span class="AppCommand">Today is a wonderful day</span>

Follow these steps to define and use the <span class="CodeFont">word\_limiter</span> function:

1.  Define inputs and outputs

    We have two inputs:

    -   the sentence that we want to limit
    -   the number of words we want to limit the output to

    The output is a string that contains the limited words.

2.  Create the shell of our Java class.

    We create a class named <span class="CodeFont">ExampleStringFunctions</span> in the package <span class="CodeFont">com.splicemachine.examples</span>.

    ``` Example
    package com.splicemachine.example;

    public class ExampleStringFunctions {
    ...
    }
    ```

3.  Create the <span class="CodeFont">wordLimiter</span> static method

    This method contains the logic for returning the first n number of words:

4.  Compile the class and store the jar file

    After you compile your class, make sure that the jar file is in a directory in your <span class="CodeFont">classpath</span>, so that it can be found. You can find more information about this in the [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) topic in this section.

    If you're using the standalone version of Splice Machine, you can use the following command line interface command:

    ``` AppCommand
    splice> CALL SQLJ.INSTALL_JAR('/Users/me/dev/workspace/examples/bin/example.jar', 'SPLICE.MY_EXAMPLE_APP', 0);
    ```

    You must also update the database class path:

    ``` AppCommand
    splice> CALL SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.MY_EXAMPLE_APP');
    ```

5.  Define the function in Splice Machine

    You can find the complete syntax for <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html)</span> in the <span class="ItalicFont">Splice Machine SQL Reference</span> manual. For our example function, we enter the following command at the <span class="CodeFont">splice&gt;</span> prompt:

    ``` AppCommand
    splice> CREATE FUNCTION WORD_LIMITER(MY_SENTENCE VARCHAR(9999), NUM_WORDS INT) RETURNS VARCHAR(9999)
    LANGUAGE JAVA
    PARAMETER STYLE JAVA
    NO SQL
    EXTERNAL NAME 'com.splicemachine.example.ExampleStringFunctions.wordLimiter';
    ```

6.  Run the function

    You can run the function with this syntax:

    ``` AppCommand
    splice> SELECT WORD_LIMITER('Today is a wonderful day and I am looking forward to going to the beach.', 5)
       FROM SYSIBM.SYSDUMMY1;
    ```

[]()Creating and Using a Sample Stored Procedure in Splice Machine
------------------------------------------------------------------

In this section , we create a stored procedure named <span class="CodeFont">GET\_INVENTORY\_FOR\_SKU</span> that retrieves all of the inventory records for a specific product by using the product's sku code. The input to this procedure is the sku code, and the output is a resultset of records from the inventory table.

Follow these steps to define and use the <span class="CodeFont">GET\_INVENTORY\_FOR\_SKU</span> function:

1.  Create and populate the inventory table

    Connect to Splice Machine and create the following table from the command prompt or from an SQL client, using the following statements:

    ``` AppCommand
    CREATE TABLE INVENTORY (
       SKU_CODE VARCHAR(30),
       WAREHOUSE BIGINT,
       QUANTITY BIGINT
    );

    INSERT INTO INVENTORY VALUES ('ABC123',1,50),('ABC123',2,100),('ABC123',3,60),('XYZ987',1,20),('XYZ321',2,0); 
    ```

2.  Create the shell of our Java class.

    We create a class named <span class="CodeFont">ExampleStringFunctions</span> in the package <span class="CodeFont">com.splicemachine.examples</span>.

    ``` Example
    package com.splicemachine.example;

    public class ExampleStoredProcedure{
    ...
    }
    ```

3.  Create the <span class="CodeFont">getSkuInventory</span> static method

    This method contains the logic for retrieving inventory records for the specified sku.

4.  Compile the class and store the jar file

    After you compile your class, make sure that the jar file is in a directory in your <span class="CodeFont">classpath</span>, so that it can be found. You can find more information about this in the [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) topic in this section.

    If you're using the standalone version of Splice Machine, you can use the following command line interface command:

    ``` AppCommand
    splice> CALL SQLJ.INSTALL_JAR('/Users/me/dev/workspace/examples/bin/example.jar', 'SPLICE.GET_SKU_INVENTORY', 0);
    ```

    You must also update the database class path:

    ``` AppCommand
    splice> CALL SYSCS_UTIL.SYSCS_SET_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.GET_SKU_INVENTORY');
    ```

5.  Define the procedure in Splice Machine

    For our procedure, we enter the following command at the <span class="CodeFont">splice&gt;</span> prompt:

    ``` AppCommand
    splice> CREATE PROCEDURE GET_INVENTORY_FOR_SKU(SKU_CODE VARCHAR(30))
    LANGUAGE JAVA
    PARAMETER STYLE JAVA
    READS SQL DATA
    EXTERNAL NAME 'com.splicemachine.example.ExampleStoredProcedure.getSkuInventory';
    ```

6.  Run the stored procedure

    You can run the procedure with this syntax:

    ``` AppCommand
    splice> call GET_INVENTORY_FOR_SKU('ABC123');
    ```

 


