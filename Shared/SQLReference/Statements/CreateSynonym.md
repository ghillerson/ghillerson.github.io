[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateSynonym.html)

<a href="" id="Statements.CreateSynonym"></a>[]()CREATE SYNONYM
===============================================================

The <span class="CodeFont">CREATE SYNONYM</span> statement allows you to create an alternate name for a table or a view.

Syntax

``` FcnSyntax
CREATE SYNONYM( synonymName FOR { viewName | tableName } );
```

synonymName

An [SQLIdentifier](../Identifiers/Intro.Identifiers.html), which can optionally include a schema name. This is the new name you want to create for the view or table.

viewName

An [SQLIdentifier](../Identifiers/Intro.Identifiers.html) that identifies the view for which you are creating a synonym.

tableName

An [SQLIdentifier](../Identifiers/Intro.Identifiers.html) that identifies the table for which you are creating a synonym.

Usage

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Currently, you can only use a synonym instead of the original qualified table or view name in these statements: <span class="CodeFont">[SELECT](Select.html)</span>, <span class="CodeFont">[INSERT](Insert.html)</span>, <span class="CodeFont">[UPDATE](UpdateTable.html)</span>,or <span class="CodeFont">[DELETE](Delete.html)</span>.

Here are a few other important notes about using synonyms:

-   Synonyms share the same name space as tables or views. You cannot create a synonym with the same name as a table that already exists in the same schema. Similarly, you cannot create a table or view with a name that matches a synonym already present.
-   You can create a synonym for a table or view that does not yet exist; however, you can only use the synonym if the table or view is present in your database.
-   You can create synonyms for other synonyms (nested synonyms); however, an error will occur if you attempt to create a synonym that results in a circular reference.
-   You cannot create synonyms in system schemas. Any schema that starts with <span class="CodeFont">SYS</span> is a system schema.
-   You cannot define a synonym for a temporary table.

Example

``` Example
splice> CREATE SYNONYM Hitting FOR Batting;
0 rows inserted/updated/deleted

splice> SELECT ID, Games FROM Batting WHERE ID < 11;
ID    |GAMES
-------------
1     |150
2     |137
3     |100
4     |143
5     |149
6     |93
7     |133
8     |52
9     |115
10    |100

0 rows inserted/updated/deleted

splice> SELECT ID, Games FROM Hitting WHERE ID < 11;
ID    |GAMES
-------------
1     |150
2     |137
3     |100
4     |143
5     |149
6     |93
7     |133
8     |52
9     |115
10    |100

0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">DROP\_SYNONYM</span>](DropSynonym.html) statement
-   <span class="CodeFont">[SHOW SYNONYMS](../../CmdLineReference/CmdShowSynonyms.html)</span> command in our <span class="ItalicFont">Developer's Guide</span>.

 


