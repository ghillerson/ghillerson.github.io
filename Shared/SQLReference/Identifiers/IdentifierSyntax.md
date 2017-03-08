[Open topic with navigation](../../../index.html#Shared/SQLReference/Identifiers/IdentifierSyntax.html)

[]()SQL Identifier Syntax
=========================

An SQLIdentifier is a dictionary object identifier that conforms to the rules of ANSI SQL; identifiers for dictionary objects:

-   are limited to 128 characters
-   are automatically translated into uppercase by the system, making them case-insensitive unless delimited by double quotes
-   cannot be a [Splice Machine SQL keyword](../ReservedWords/SQLReservedWords.html) unless delimited by double quotes
-   can sometimes be qualified by a schema, table, or correlation name, as described below

Examples:

This view name:

``` Example
CREATE VIEW PitchingCoaches(RECEIVED) AS VALUES 1;
```

is stored in system catalogs as <span class="CodeFont">PITCHINGCOACHES</span>, since it is not quoted.

Whereas this view name:

``` Example
CREATE VIEW "PitchingCoaches"(RECEIVED) AS VALUES 1;
```

is quoted, and thus is stored as <span class="CodeFont">PitchingCoaches</span> in the system catalog

Qualifying dictionary objects

Since some dictionary objects can be contained within other objects, you can qualify those dictionary object names. Each component is separated from the next by a period (<span class="CodeFont">.</span>). You qualify a dictionary object name in order to avoid ambiguity.

Examples:

Here is an example of a simple, unqualified SQLIdentifier used to name a table:

``` Example
CREATE TABLE Coaches( ID INT NOT NULL );
```

And here's an example of a table name (<span class="CodeFont">Coaches</span>) qualified by a schema name (<span class="CodeFont">Baseball</span>):

``` Example
CREATE TABLE Baseball.Coaches( ID INT NOT NULL );
```

<a href="" id="SQL92Rules"></a>Rules for SQL Identifiers

Here are some additional rules that apply to SQLIdentifiers:

-   Ordinary identifiers are identifiers not surrounded by double quotation marks:

    -   An ordinary identifier must begin with a letter and contain only letters, underscore characters (<span class="CodeFont">\_</span>), and digits.
    -   All Unicode letters and digits are permitted; however, Splice Machine does not attempt to ensure that the characters in identifiers are valid in the database's locale.
-   Delimited identifiers are identifiers surrounded by double quotation marks:

    -   A delimited identifier can contain any characters within the double quotation marks.
    -   The enclosing double quotation marks are not part of the identifier; they serve only to mark its beginning and end.
    -   Spaces at the end of a delimited identifier are truncated.
    -   You can use two consecutive double quotation marks within a delimited identifier to include a double quotation mark within the identifier.

[]()[]()Capitalization and Special Characters in SQL Statements
---------------------------------------------------------------

You can submit SQL statements to Splice Machine as strings by using JDBC; these strings use the Unicode character set. Within these strings:

-   Double quotation marks delimit special identifiers referred to in ANSI SQL as <span class="ItalicFont">delimited identifiers</span>.
-   Single quotation marks delimit character strings.
-   Within a character string, to represent a single quotation mark or apostrophe, use two single quotation marks. (In other words, a single quotation mark is the escape character for a single quotation mark).
-   SQL keywords are case-insensitive. For example, you can type the keyword <span class="CodeFont">SELECT</span> as <span class="CodeFont">SELECT</span>, <span class="CodeFont">Select</span>, <span class="CodeFont">select</span>, or <span class="CodeFont">sELECT</span>.
-   ANSI SQL -style identifiers are case-insensitive unless they are delimited.
-   Java-style identifiers are always case-sensitive.

### Other Special Characters:

-   <span class="CodeFont">\*</span> is a wildcard within a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html).</span>; see [The \* wildcard](../Expressions/Select.html#StarWildcard). It can also be the multiplication operator. In all other cases, it is a syntactical metasymbol that flags items you can repeat 0 or more times.
-   <span class="CodeFont">%</span> and <span class="CodeFont">\_</span> are character wildcards when used within character strings following a <span class="CodeFont">LIKE</span> operator (except when escaped with an escape character). See [Boolean expressions](../Expressions/BooleanExpressions.html).
-   Comments can be either single-line or multi-line, as per the ANSI SQL standard:

    -   Single line comments start with two dashes (<span class="CodeFont">--</span>) and end with the newline character.
    -   Multi-line comments are bracketed and start with forward slash star (<span class="CodeFont">/\*</span>), and end with star forward slash (<span class="CodeFont">\*/</span>). Note that bracketed comments may be nested. Any text between the starting and ending comment character sequence is ignored.

 


