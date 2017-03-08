[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/DataTypeCompatability.html)

<a href="" id="DataTypes.Assignments"></a>Splice Machine []()Data Assignments and Comparisons
=============================================================================================

The following table displays valid assignments between data types in Splice Machine. A <span class="ItalicFont">Y</span> indicates that the assignment is valid.

| TYPES             | B   
                     O    
                     O    
                     L    
                     E    
                     A    
                     N    | S   
                           M    
                           A    
                           L    
                           L    
                           I    
                           N    
                           T    | I   
                                 N    
                                 T    
                                 E    
                                 G    
                                 E    
                                 R    | B   
                                       I    
                                       G    
                                       I    
                                       N    
                                       T    | D   
                                             E    
                                             C    
                                             I    
                                             M    
                                             A    
                                             L    | R   
                                                   E    
                                                   A    
                                                   L    | D   
                                                         O    
                                                         U    
                                                         B    
                                                         L    
                                                         E    | F   
                                                               L    
                                                               O    
                                                               A    
                                                               T    | C   
                                                                     H    
                                                                     A    
                                                                     R    | V   
                                                                           A    
                                                                           R    
                                                                           C    
                                                                           H    
                                                                           A    
                                                                           R    | L   
                                                                                 O    
                                                                                 N    
                                                                                 G    
                                                                                 V    
                                                                                 A    
                                                                                 R    
                                                                                 C    
                                                                                 H    
                                                                                 A    
                                                                                 R    | C   
                                                                                       L    
                                                                                       O    
                                                                                       B    
                                                                                       /    
                                                                                       T    
                                                                                       E    
                                                                                       X    
                                                                                       T    | B   
                                                                                             L    
                                                                                             O    
                                                                                             B    | D   
                                                                                                   A    
                                                                                                   T    
                                                                                                   E    | T   
                                                                                                         I    
                                                                                                         M    
                                                                                                         E    | T   
                                                                                                               I    
                                                                                                               M    
                                                                                                               E    
                                                                                                               S    
                                                                                                               T    
                                                                                                               A    
                                                                                                               M    
                                                                                                               P    | U   
                                                                                                                     s    
                                                                                                                     e    
                                                                                                                     r    
                                                                                                                     -    
                                                                                                                     d    
                                                                                                                     e    
                                                                                                                     f    
                                                                                                                     i    
                                                                                                                     n    
                                                                                                                     e    
                                                                                                                     d    
                                                                                                                          
                                                                                                                     t    
                                                                                                                     y    
                                                                                                                     p    
                                                                                                                     e    |
|-------------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| BOOLEAN           | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| SMALLINT          | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| INTEGER           | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| BIGINT            | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| DECIMAL           | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| REAL              | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| DOUBLE            | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| FLOAT             | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| CHAR              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | Y   | Y   | Y   | -   |
| VARCHAR           | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | Y   | Y   | Y   | -   |
| LONG VARCHAR      | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   |
| CLOB / TEXT       | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   |
| BLOB              | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | Y   | -   | -   | -   | -   |
| DATE              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | -   | -   | -   |
| TIME              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | -   | Y   | -   | -   |
| TIMESTAMP         | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | -   | -   | Y   | -   |
| User-defined type | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | Y   |

A value of a user-defined type can be assigned to a value of any supertype of that user-defined type. However, no explicit casts of user-defined types are allowed.

The following table displays valid comparisons between data types in Splice Machine. A <span class="ItalicFont">Y</span> indicates that the comparison is allowed.

| TYPES             | B   
                     O    
                     O    
                     L    
                     E    
                     A    
                     N    | S   
                           M    
                           A    
                           L    
                           L    
                           I    
                           N    
                           T    | I   
                                 N    
                                 T    
                                 E    
                                 G    
                                 E    
                                 R    | B   
                                       I    
                                       G    
                                       I    
                                       N    
                                       T    | D   
                                             E    
                                             C    
                                             I    
                                             M    
                                             A    
                                             L    | R   
                                                   E    
                                                   A    
                                                   L    | D   
                                                         O    
                                                         U    
                                                         B    
                                                         L    
                                                         E    | F   
                                                               L    
                                                               O    
                                                               A    
                                                               T    | C   
                                                                     H    
                                                                     A    
                                                                     R    | V   
                                                                           A    
                                                                           R    
                                                                           C    
                                                                           H    
                                                                           A    
                                                                           R    | L   
                                                                                 O    
                                                                                 N    
                                                                                 G    
                                                                                 V    
                                                                                 A    
                                                                                 R    
                                                                                 C    
                                                                                 H    
                                                                                 A    
                                                                                 R    | C   
                                                                                       L    
                                                                                       O    
                                                                                       B    
                                                                                       /    
                                                                                       T    
                                                                                       E    
                                                                                       X    
                                                                                       T    | B   
                                                                                             L    
                                                                                             O    
                                                                                             B    | D   
                                                                                                   A    
                                                                                                   T    
                                                                                                   E    | T   
                                                                                                         I    
                                                                                                         M    
                                                                                                         E    | T   
                                                                                                               I    
                                                                                                               M    
                                                                                                               E    
                                                                                                               S    
                                                                                                               T    
                                                                                                               A    
                                                                                                               M    
                                                                                                               P    | U   
                                                                                                                     s    
                                                                                                                     e    
                                                                                                                     r    
                                                                                                                     -    
                                                                                                                     d    
                                                                                                                     e    
                                                                                                                     f    
                                                                                                                     i    
                                                                                                                     n    
                                                                                                                     e    
                                                                                                                     d    
                                                                                                                          
                                                                                                                     t    
                                                                                                                     y    
                                                                                                                     p    
                                                                                                                     e    |
|-------------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| BOOLEAN           | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| SMALLINT          | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| INTEGER           | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| BIGINT            | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| DECIMAL           | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| REAL              | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| DOUBLE            | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| FLOAT             | -   | Y   | Y   | Y   | Y   | Y   | Y   | Y   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| CHAR              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | Y   | Y   | -   |
| VARCHAR           | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | Y   | Y   | -   |
| LONG VARCHAR      | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| CLOB / TEXT       | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| BLOB              | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |
| DATE              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | Y   | -   | -   | -   |
| TIME              | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | -   | Y   | -   | -   |
| TIMESTAMP         | -   | -   | -   | -   | -   | -   | -   | -   | Y   | Y   | -   | -   | -   | -   | -   | Y   | -   |
| User-defined type | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   | -   |

 


