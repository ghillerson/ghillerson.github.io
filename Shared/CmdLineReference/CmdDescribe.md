[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdDescribe.html)

[]()Describe Command
====================

The <span class="AppCommand">describe</span> command displays a description of the specified table or view.

Syntax

``` FcnSyntax
DESCRIBE { table-Name | view-Name }
```

tableName

The name of the table whose description you want to see.

viewName

The name of the view whose description you want to see.

Results

The <span class="AppCommand">describe</span> command results contains the following columns:

| Column Name      | Description                                                          |
|------------------|----------------------------------------------------------------------|
| COLUMN\_NAME     | The name of the column                                               |
| TYPE\_NAME       | The data type of the column                                          |
| DECIMAL\_DIGITS  | The number of fractional digits                                      |
| NUM\_PREC\_RADIX | The radix, which is typically either 10 or 2                         |
| COLUMN\_SIZE     | The column size:                                                     
                                                                                          
                    -   For char or date types, this is the maximum number of characters  
                    -   For numeric or decimal types, this is the precision               |
| COLUMN\_DEF      | The default value for the column                                     |
| CHAR\_OCTE       | Maximum number of bytes in the column                                |
| IS\_NULL         | Whether (YES) or not (NO) the column can contain null values         |

Examples

``` AppCommand
splice> describe T_DETAIL;
COLUMN_NAME                 |TYPE_NAME|DEC |NUM |COLUM |COLUMN_DEF|CHAR_OCTE |IS_NULL
--------------------------------------------------------------------------------------------------
TRANSACTION_HEADER_KEY      |BIGINT   |0   |10  |19    |NULL      |NULL      |NO      
TRANSACTION_DETAIL_KEY      |BIGINT   |0   |10  |19    |NULL      |NULL      |NO      
CUSTOMER_MASTER_ID          |BIGINT   |0   |10  |19    |NULL      |NULL      |YES     
TRANSACTION_DT              |DATE     |0   |10  |10    |NULL      |NULL      |NO      
ORIGINAL_SKU_CATEGORY_ID    |INTEGER  |0   |10  |10    |NULL      |NULL      |YES     

5 rows selected
```

 


