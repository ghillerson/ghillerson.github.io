[Open topic with navigation](../../../index.html#Shared/SQLReference/Identifiers/Intro.Identifiers.html)

[]()Identifiers
===============

This section contains the reference documentation for the Splice Machine SQL Identifiers, in these topics:

-   This page provides an introduction to <span class="CodeFont">SQLIdentifiers</span>.
-   The [SQL Identifier Syntax](IdentifierSyntax.html) topic contains additional information about <span class="CodeFont">SQLIdentifier</span> naming rules, capitalization, and special characters.
-   The [SQL Identifier Types](IdentifierTypes.html) topic provides specific information about the different types of <span class="CodeFont">SQLIdentifiers</span> that you'll find mentioned in this manual, including:

    -   AuthorizationIdentifier
    -   column-Name and simple-column-Name
    -   constraint-Name
    -   correlation-Name
    -   index-Name
    -   new-Table-Name
    -   RoleName
    -   schemaName
    -   synonym-Name
    -   table-Name
    -   triggerName
    -   view-Name

[]()About SQLIdentifiers
------------------------

An SQLIdentifier is a dictionary object identifier that conforms to the rules of ANSI SQL; identifiers for dictionary objects:

-   are limited to 128 characters
-   are automatically translated into uppercase by the system, making them case-insensitive unless delimited by double quotes
-   cannot be a [Splice Machine SQL keyword](../ReservedWords/SQLReservedWords.html) unless delimited by double quotes
-   can sometimes be qualified by a schema, table, or correlation name, as described below

Examples:

Here is an example of a simple, unqualified SQLIdentifier used to name a table:

``` Example
CREATE TABLE Coaches( ID INT NOT NULL );
```

And here's an example of a table name (<span class="CodeFont">Coaches</span>) qualified by a schema name (<span class="CodeFont">Baseball</span>):

``` Example
CREATE TABLE Baseball.Coaches( ID INT NOT NULL );
```

This view name is stored in system catalogs as <span class="CodeFont">PITCHINGCOACHES</span>, since it is not quoted:

``` Example
CREATE VIEW PitchingCoaches(RECEIVED) AS VALUES 1;
```

Whereas this view name is quoted, and thus is stored as <span class="CodeFont">PitchingCoaches</span> in the system catalog:

``` Example
CREATE VIEW "PitchingCoaches"(RECEIVED) AS VALUES 1;
```

Complete syntax, including information about case sensitivity and special character usage, in SQL Identifier types is found in the [SQL Identifier Syntax](IdentifierSyntax.html) topic in this section.

 


