[Open topic with navigation](../../index.html#OnPremise/GettingStarted/ExamplesDatabase.html)

About Our Documentation Examples Database
=========================================

This topic describes the database that we have created to provide code examples throughout our documentation suite. We've pulled in basic seasonal statistics for two Major League Baseball teams, though all names have been changed. We're calling this our []()<span class="AppCommand">DocsExamplesDb</span> database.

Our <span class="AppCommand">DocsExamplesDb</span> database features these tables:

| Table                                  | Contains                                                       |
|----------------------------------------|----------------------------------------------------------------|
| <span class="BoldFont">Players</span>  | The player's name, ID, and other general information.          |
| <span class="BoldFont">Salaries</span> | The salary for each player ID for each season.                 |
| <span class="BoldFont">Batting</span>  | Batting statistics, per season, for each player ID.            |
| <span class="BoldFont">Fielding</span> | Fielding statistics, per season, for each player ID.           |
| <span class="BoldFont">Pitching</span> | Pitching statistics, per season, for each pitcher's player ID. |

The tables were populated with data found on the Internet, primarily from the [baseball-reference.com](http://www.baseball-reference.com/) site.

If you want to import these tables into your Splice Machine database to try any examples yourself, follow the simple instructions in the <a href="#Importin" class="selected">Importing the Documentation Examples Database</a> at the end of this topic.

Table Schemas
-------------

Our example tables are all stored in a schema named <span class="CodeFont">SPLICEBBALL</span>. This section describes the fields in each of our <span class="AppCommand">DocsExamplesDb</span> tables.

### The Players Table

The <span class="AppCommand">SPLICEBBALL.Players</span> table contains these columns:

| Column Name | Type     | Description                                                         |
|-------------|----------|---------------------------------------------------------------------|
| ID          | SMALLINT | The unique player ID, assigned upon insertion.                      |
| Team        | VARCHAR  | The abbreviated name of the player's team.                          |
| DisplayName | VARCHAR  | The name we use when displaying this player.                        |
| Position    | CHAR(2)  | The abbreviation for the player's main position, e.g. P, C, OF, 1B. |
| Birthdate   | DATE     | The birth date of the player.                                       |

### The Salaries Table

The <span class="AppCommand">SPLICEBBALL.Salaries</span> table contains these columns:

| Column Name | Type     | Description                         |
|-------------|----------|-------------------------------------|
| ID          | SMALLINT | The unique player ID.               |
| Season      | SMALLINT | The season (year).                  |
| Salary      | BIGINT   | The player's salary for the season. |

### The Batting Table

The <span class="AppCommand">SPLICEBBALL.Batting</span> contains these columns:

| Column Name        | Type     | Description                                                      |
|--------------------|----------|------------------------------------------------------------------|
| ID                 | SMALLINT | The unique player ID.                                            |
| Season             | SMALLINT | The season (year).                                               |
| Games              | SMALLINT | The number of games in which the player batted.                  |
| PlateAppearances   | SMALLINT | The number of times the player made a plate appearance.          |
| AtBats             | SMALLINT | The number of official at bats.                                  |
| Runs               | SMALLINT | The number of runs scores.                                       |
| Hits               | SMALLINT | How many hits by the player.                                     |
| Singles            | SMALLINT | How many singles hit by the player.                              
                                                                                                   
                                 This value is computed by a triggered function.                   |
| Doubles            | SMALLINT | How many doubles hit by the player.                              |
| Triples            | SMALLINT | How many triples hit by the player.                              |
| HomeRuns           | SMALLINT | How many home runs hit by the player.                            |
| RBI                | SMALLINT | How many Runs Batted In by the player.                           |
| StolenBases        | SMALLINT | How many bases the player stole.                                 |
| CaughtStealing     | SMALLINT | How many times the player was caught attempting to steal a base. |
| Walks              | SMALLINT | The number of walks the player drew.                             |
| Strikeouts         | SMALLINT | The number of times the player walked.                           |
| DoublePlays        | SMALLINT | How many times the player hit into a double play.                |
| HitByPitches       | SMALLINT | The number of times the player was hit by a pitch.               |
| SacrificeHits      | SMALLINT | The number of sacrifice bunts the player hit.                    |
| SacrificeFlies     | SMALLINT | The number of sacrifice flies the player hit.                    |
| IntentionalWalks   | SMALLINT | The number of intentional walks issued to the player.            |
| Average            | DECIMAL  | The player's batting average.                                    
                                                                                                   
                                 This value is computed by a triggered function.                   |
| TotalBases         | SMALLINT | The total number of bases for the player.                        
                                                                                                   
                                 This value is computed by a triggered function.                   |
| OnBasePercentage   | DECIMAL  | The percentage of times the player reached base.                 
                                                                                                   
                                 This value is computed by a triggered function.                   |
| Slugging           | DECIMAL  | The slugging average of the player.                              
                                                                                                   
                                 This value is computed by a triggered function.                   |
| OnBasePlusSlugging | DECIMAL  | The OPS for the player.                                          
                                                                                                   
                                 This value is computed by a triggered function.                   |

### The Fielding Table

The <span class="AppCommand">SPLICEBBALL.Fielding</span> table contains these columns:

| Column Name                    | Type     | Description                                                                                              |
|--------------------------------|----------|----------------------------------------------------------------------------------------------------------|
| ID                             | SMALLINT | The unique player ID.                                                                                    |
| Season                         | SMALLINT | The season (year).                                                                                       |
| FldGames                       | SMALLINT | How many games the player was in the field for.                                                          |
| Chances                        | SMALLINT | The number of fielding chances the player had.                                                           |
| Putouts                        | SMALLINT | The number of putouts the player had.                                                                    |
| Assists                        | SMALLINT | The number of assists the player had.                                                                    |
| Errors                         | SMALLINT | The number of errors committed by the player.                                                            |
| FldDoublePlays                 | SMALLINT | The number of doubles plays in which the player was involved in as a fielder.                            |
| Percentage                     | DECIMAL  | The percentage of opportunities for outs that the player successfully completed.                         |
| TZAboveAverage                 | SMALLINT | A fielding metric: total zone runs above average for his position.                                       |
| TZAboveAveragePer1200          | SMALLINT | Total zone runs extrapolated for 1200 innings.                                                           |
| RunsSaved                      | SMALLINT | The number of runs saved in the field by the player.                                                     |
| RunsSavedAboveAvg              | SMALLINT | The number of runs saved by the player over the average number saved for his position.                   |
| RangeFactorPerNine             | DECIMAL  | A fielding metric that evaluates the average number of putouts and assists per nine innings,             |
| RangeFactorPerGame             | DECIMAL  | A fielding metric that evaluates the average number of putouts and assists per game played,              |
| PassedBalls                    | SMALLINT | The number of passed balls for catchers.                                                                 |
| WildPitches                    | SMALLINT | The number of wild pitches for pitchers.                                                                 |
| FldStolenBases                 | SMALLINT | The number of stolen bases given up by a pitcher or catcher.                                             |
| FldCaughtStealing              | SMALLINT | The number of players caught stealing by a pitcher or catcher.                                           |
| FldCaughtStealingPercent       | DECIMAL  | For catchers and pitchers, the percentage of attempted stolen bases that were successful.                |
| FldLeagueCaughtStealingPercent | DECIMAL  | For pitchers and catchers, the league average percentage of attempted stolen bases that were successful. |
| Pickoffs                       | SMALLINT | For pitchers and catchers, the number of runners picked off.                                             |
| FldInnings                     | DECIMAL  | The number of innings in which the player was in the field.                                              |

### The Pitching Table

The <span class="AppCommand">SPLICEBBALL.Pitching</span> table contains these fields:

| Column Name         | Type     | Description                                                                                                                                              |
|---------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID                  | SMALLINT | The unique player ID.                                                                                                                                    |
| Season              | SMALLINT | The season (year).                                                                                                                                       |
| Wins                | SMALLINT | How many games the pitcher won.                                                                                                                          |
| Losses              | SMALLINT | How many games the pitcher lost.                                                                                                                         |
| Games               | SMALLINT | The number of games in which the pitcher appeared.                                                                                                       |
| GamesStarted        | SMALLINT | The number of games the pitcher started.                                                                                                                 |
| GamesFinished       | SMALLINT | The number of games the pitcher finished.                                                                                                                |
| CompleteGames       | SMALLINT | The number of complete games by the pitcher.                                                                                                             |
| Shutouts            | SMALLINT | The number of shutout games thrown by the pitcher.                                                                                                       |
| Saves               | SMALLINT | The number of games saved by the pitcher.                                                                                                                |
| Innings             | DECIMAL  | The number of innings pitched.                                                                                                                           |
| Hits                | SMALLINT | The number of hits given up by the pitcher.                                                                                                              |
| Runs                | SMALLINT | The number of runs give up by the pitcher.                                                                                                               |
| EarnedRuns          | SMALLINT | The number of earned runs give up by the pitcher.                                                                                                        |
| HomeRuns            | SMALLINT | How many homeruns the pitcher gave up.                                                                                                                   |
| Walks               | SMALLINT | How many walks the pitcher issued.                                                                                                                       |
| IntentionalWalks    | SMALLINT | How many intentional walks the pitcher issued.                                                                                                           |
| Strikeouts          | SMALLINT | How many batters the pitchers struck out.                                                                                                                |
| HitBatters          | SMALLINT | How many batters the pitcher hit with a pitch.                                                                                                           |
| Balks               | SMALLINT | How many balks the pitcher committed.                                                                                                                    |
| WildPitches         | SMALLINT | How many wild pitches were thrown by the pitcher.                                                                                                        |
| BattersFaced        | SMALLINT | The number of batters faced by the pitcher.                                                                                                              |
| FieldingIndependent | DECIMAL  | A metric (FIP) for pitchers that determines the quality of a pitcher's performance by eliminating plate appearance outcomes that involve defensive play. |
| ERA                 | DECIMAL  | The pitcher's earned run average.                                                                                                                        
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| WHIP                | DECIMAL  | The number of walks and hits per inning pitched by the player.                                                                                           
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| HitsPerNine         | DECIMAL  | The number of hits per nine innings pitched by the player.                                                                                               
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| HomeRunsPerNine     | DECIMAL  | The number of home runs per nine innings pitched by the player.                                                                                          
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| WalksPerNine        | DECIMAL  | The number of walks per nine innings pitched by the player.                                                                                              
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| StrikeoutsPerNine   | DECIMAL  | The number of strikeouts per nine innings pitched by the player.                                                                                         
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |
| StrikeoutsToWalks   | DECIMAl  | The ratio of strikeouts to walks thrown by the pitcher.                                                                                                  
                                                                                                                                                                                            
                                  This value is computed by a triggered function.                                                                                                           |

[]()Importing the Documentation Examples Database
-------------------------------------------------

This topic describes how to import our documentation database tables into your database, if you want to try any of the examples. Follow these steps to import the tables into your database:

1.  Download the [Documentation Examples Database](../../Resources/DocExamplesDb/2.0/DocExamplesDb.tar.gz) tarball and copy it to your <span class="AppCommand">splicemachine</span> directory.
2.  Decompress the tarball with the following command:

    ``` Example
    tar -xvf DocExamplesDb.tar.gz
    ```

3.  If Splice Machine is not yet started, start it; for example:

    ``` AppCommand
    ./bin/start-splice.sh
    splicemachine/bin/sqlshell.sh
    ```

4.  At the splice&gt; prompt, run the sql commands to create the SPLICEBBALL scheam, and to create and import data into the doc examples database:

    ``` AppCommand
    splice> run 'DocExamplesDb/CreateDocExamplesDb.sql';
    ```

5.  Verify that the examples tables have been created:

    ``` AppCommand
    splice> show tables in SPLICEBBALL;
    ```

    The list of tables should include these tables:

    ``` AppCommand
    BATTING
    FIELDING
    PITCHING
    PLAYERS
    SALARIES
    ```

You can use the <span class="CodeFont">SET SCHEMA</span> command to set the current schema to <span class="CodeFont">SPLICEBBALL</span> if you want to run SQL operations without explicitly specifying the schema:
       <span class="AppCommand">splice&gt; SET SCHEMA SPLICEBBALL;</span>

 


