[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateSchema.html)

<a href="" id="Statements.CreateSchema"></a>[]()CREATE SCHEMA
=============================================================

The <span class="CodeFont">CREATE SCHEMA</span> statement allows you to create a database schema, which is a way to logically group objects in a single collection and provide a unique name-space for those objects.

Syntax

``` FcnSyntax
CREATE SCHEMA {
     [ schemaName ] 
     }
```

The <span class="CodeFont">CREATE SCHEMA</span> statement is used to create a schema. A schema name cannot exceed <span class="CodeFont">128</span> characters. Schema names must be unique within the database.

A schema name cannot start with the prefix <span class="CodeFont">SYS</span> (after case normalization). Use of the prefix <span class="CodeFont">SYS</span> raises a <span class="ItalicFont">SQLException</span>.

CREATE SCHEMA examples

To create a schema for airline-related tables, use the following syntax:

``` Example
splice> CREATE SCHEMA FLIGHTS;
0 rows inserted/updated/deleted
```

To create a schema employee-related tables, use the following syntax:

``` Example
splice> CREATE SCHEMA EMP;
0 rows inserted/updated/deleted
```

To create a table called availability in the EMP and FLIGHTS schemas, use the following syntax:

``` Example
splice> CREATE TABLE Flights.Availability(
   Flight_ID CHAR(6) NOT NULL,
   Segment_Number INT NOT NULL,
   Flight_Date DATE NOT NULL, 
   Economy_Seats_Taken INT,
   Business_Seats_Taken INT, 
   FirstClass_Seats_Taken INT, 
   CONSTRAINT Flt_Avail_PK
   PRIMARY KEY (Flight_ID, Segment_Number, Flight_Date)
   );
0 rows inserted/updated/deleted

splice> CREATE TABLE EMP.AVAILABILITY(
   Hotel_ID INT NOT NULL,
   Booking_Date DATE NOT NULL,
   Rooms_Taken INT,
   CONSTRAINT HotelAvail_PK PRIMARY KEY (Hotel_ID, Booking_Date)
   );   
0 rows inserted/updated/deleted
```

See Also

-   <span class="CodeFont">[DROP SCHEMA](DropSchema.html)</span> statement
-   [Schema Name](../Identifiers/IdentifierTypes.html#SchemaName)
-   <span class="CodeFont">[SET SCHEMA](SetSchema.html)</span> statement

 


