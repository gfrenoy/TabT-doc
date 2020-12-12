---
layout: default
title: Upload
nav_order: 2
---

# Upload
{: .no_toc }

In order to allow other applications to send data into TabT, and to ensure [interoperability](http://en.wikipedia.org/wiki/Interoperability) with applications based on TabT data, an upload format is provided.

This upload format is based on the use of simple text files that can easily be verified by humans.

## General
{: .no_toc }

An upload file is a text file composed of lines and columns.

**Line separator** : line end (ASCII 13) or carriage return (ASCII 10 + ASCII 13)

**Column separator** : semi column (;)

## First column
{: .no_toc }

The first column determines the type of information that will be sent to the server. It consists of one or two characters. Possible values are:

{:toc}

- ToC


## Line "C" : Heading or comments

This line defines a free comment and is ignored.  The number and contents of the next columns are free.

Example
{: .label .label-blue }

```
C;This is a free comment;With several columns;All ignored
```

## Line "I" : Change in a result of a team match (aka interclub)

With this line type interclub results are uploaded. It needs the following columns :

- Season of the match ;
- Match identifier ;
- Home club ;
- Visiting club ;
- Home players list;
- Visiting players list;

### Season
{: .no_toc }

The identifier is a number which corresponds with a season:

* 5 = 2004-2005
* 6 = 2005-2006
* 7 = 2006-2007
* etc.

### Match identifier
{: .no_toc }

Unique identifier of the match for which the results will be uploaded.

This number is the same as the one given by the TabT application.

Examples
{: .label .label-blue }

```NH03/031```, ```PWVLD09/183``` or ```PVLBH17/019```.

### Home club
{: .no_toc }

Home club index or "bye" if the visiting team does not play a match this week (but still has to send a team composition).

### Visiting club
{: .no_toc }

Same as home club but for the visiting club.

### Home players list
{: .no_toc }

The list of affiliation numbers of the home players who play the match.
This list consists of maximum four numbers of 6 characters, separated by a comma (,).

If the player affiliation number is preceded by a dash (-), the player is W-O for all matches.  If the player affiliation number is not know, it must be replaced by a question mark (?).
The number of players has to be equal to the number of players determined for this match.

This column may be completely empty if a result type 'U' is used (see below).

If there are one or more double matches, the list will consist of one or more extra elements, containing the composition of the dubbel team(s).
This composition consists of :

- The number of the first double player
- a dash (-)
- The number of the second double player

These numbers have to be inferior or equal to the number of players in the team.

### Visiting players list
{: .no_toc }

Same as for the visiting teams.  The number of players and the number of double teams have to be equal in both teams.

### Match results
{: .no_toc }

There are three possibilities.  The first letter of this column indicates the used method :

- **S** : Only the final match result (in sets) is provided.
- **P** : All match points are provided
- **U** : Only the final result is provided (without details)

**Individual results in sets ("S")**

The column starts with 'S'.

This letter is followed by a sequence of numbers between 0 and 9 or dashes (-). Every character represents the result of an individual match:

* 0 = Victory 0-3 (or 0-4) of the visiting player
* 1 = Victory 1-3 (or 1-4) of the visiting player
* 2 = Victory 2-3 (or 2-4) of the visiting player
* 3 = Victory 3-0 (or 4-0) of the home player
* 4 = Victory 3-1 (or 4-1) of the home player
* 5 = Victory 3-2 (or 4-2) of the home player
* 6 = Victory 3-4 of the visiting player
* 7 = Victory 4-3 of the home player
* 8 = W-O of the home player = victory of the visiting player
* 9 = W-O of the visiting player = victory of the home player
* dash (-) = W-O of both the home and the visiting player

The number of characters must correspond with the number of individual matches in the team match.

Examples
{: .label .label-blue }

```S0403502540950509```, ```S4143443441445345``` or ```S9999999999999999```.

**Individual results in points ("P")**

The column starts with 'P'.

This letter is followed by a list of individual match results seperated by commas (,).  The number of individual match results must be equal to the number of individual matches in the team match. In case of W-O the individual match result is :

* 8 = W-O of the home player
* 9 = W-O of the visiting player
* dash (-) = W-O of both the home and the visiting player

A match result consists of a list of match results separated by a a slash (/).  
A set result is the number of points scored by the set looser. If the visiting player wins the set, this number is preceded by a dash (-).

Example
{: .label .label-blue }

The individual match result is ```11-7 / 4-11 / 11-8 / 11-5```

This score will be represented by : ```7/-4/8/5```

**Team match score ("U")**

The column starts with 'U'.

This letter is followed by the team match score.  This result consists of :

* The number of individual matches won by the home team
* A dash (-)
* The number of individual matches won by the visiting team

Examples
{: .label .label-blue }

```15-1``` or ```7-3``` or ```6-9```.

### Responsibles
{: .no_toc }

This column is optional.

The column consists of a list of 4 player indexes, separated by commas (,).  
These players are :

* The captain of the home team
* The captain of the visiting team
* The team match referee
* The hall commissionary

The hall commissionary is optional.

### Hours
{: .no_toc }

This column is optional.

The column consists of two hour groups separated by commas (,). The format is HH:MM where HH is the number of hours and MM the number of minutes.  These two hour groups correspond with :

* The team match starting hour
* The team match ending hour

### Comments
{: .no_toc }

This column is optional.

The column starts with a double quote (") and ends with a double quote (").  The rest of the line is considered as comments.  A carriage return is replaced by the sequence "backslash-character n" (\n).  A backslash (\) is represented by a double backslash (\\).

Examples
{: .label .label-blue }

Team match [Tienen A - Werchter A](https://competitie.vttl.be/?season=6&week_name=17&sel=3&detail=1&div_id=127&club_id=0&menu=4) in first division, province of Flemish Brabant & Brussels of season 2005-2006:

```
C;Example format !TabT-Upload / match Tienen A - Werchter A
I;6;17/003;VLB330;VLB295;506080,505415,-506077,506077;505198,506082,505974,505973;S1824181008052811
```

Team match [Herckenrode A - Pingouin Leuven A](https://competitie.vttl.be/?season=6&week_name=07&sel=4&detail=1&div_id=139&club_id=0&menu=4) in regional series A (Ladies) of season 2005-2006:

```
C;Example format !TabT-Upload / match Herckenrode A - Pingouin Leuven A
I;6;L07/054;LK49;VLB5;506862,506778,506855,1-2;505256,505852,505855,1-3;S5232043505
```

Team match [Kobelco Verdinamur A-Hoeselt A](https://competitie.vttl.be/?season=6&modif=0&club_id=0&week_name=07&div_id=144), in second national division, series A of season 2005-2006:

```
C;Example format !TabT-Upload / match Kobelco Verdinamur A-Hoeselt A
I;6;N07/044;N51;LK103;;;U13-3
```

Team match [Hurricane H-TT VMS D](https://competitie.vttl.be/?season=6&menu=4&club_id=0&sel=2&div_id=133&modif=0&detail=1), in fourth provincial division, series B, province of Flemish Brabant & Brussels of season 2005-2006:

```
C;Example format !TabT-Upload / match Hurricane H - TT VMS D
I;6;19/038;VLB225;VLB318;505393,505280,505282,509986;505460,506003,505996,506008;P-9/4/5/4,9/1/3,5/7/6,7/3/8,5/4/2,8/9/8,10/-9/-7/6/-6,12/4/-5/9,4/5/5,9/2/-9/9,9/-10/2/2,8/4/9,9/8/4,-5/9/5/9,8/3/1,11/10/6;505385,505460,505385;19:45,22:45
```

When a team withdraws a match, team composition is not known by the other party and player affiliation numbers must be replaced by question marks

```
C;Example format TabT-Upload / visited team withdraws
I;10;05/131;WVL72;WVL78;?,?,?,?;500352,501728,509376,513547;P8,8,8,8,8,8,8,8,8,8,8,8,8,8,8,8
```

## Line "TR" : Change in a tournament configuration

_**TODO**_

## Line "T" : Change in a tournament result

This line allows the registration of a tournament match result.

This line type needs the next additional columns:

### Season
{: .no_toc }

Identifier of the season during which the tournament takes place (see also the same field for _Line "I"_ above).

### Tournament identifier
{: .no_toc }

Unique tournament identifier. This identifier is defined by the ''Reference'' field in the ''Tournament'' section of TabT.

If there is no defined tournament identifier, the tournament name can be used. Case, accents and spaces will be ignored.

### Categorie
{: .no_toc }

Age categorie of the match series. The categorie must correspond to the tournament definition in TabT.

Typical values are:

- POU = Poussins/Benjamins
- PRE = Preminimes
- MIN = Minimes
- CAD = Cadets
- JUN = Juniors
- J21 = Youth -21
- SEN = Seniors
- V40 = Veterans +40
- V50 = Veterans +50
- V60 = Veterans +60
- V70 = Veterans +70
- V80 = Veterans +80
- V85 = Veterans +85

### Gender
{: .no_toc }

* H : Gentlemen
* D : Ladies

The _gender_ field must correspond to the tournament definition in TabT.

### Series name
{: .no_toc }

Match series name. The name must correspond to the tournament definition in TabT. Case, accents and spaces will be ignored.

### Round number
{: .no_toc }

For a later use. For the moment this field must be empty.

### Match identifier
{: .no_toc }

Unique match identifier within the series. The identifier must be a positive number.

### Identifier player 1
{: .no_toc }

Identifier for the first player. The identifier is a 6 digit number.

### Identifier player 2
{: .no_toc }

Identifier for the second player. The identifier is a 6 digit number.

### Match result
{: .no_toc }

The match result composed of the following elements:

- The number of sets won by the first player
- a dash (-)
- The number of sets won by the second player

One of the two players must have won more sets than the other and this number must correspond to the number of sets to win defined in the series or tour configuration. The other player must have a lower number of sets, that is however higher or equal to 0.

Example
{: .label .label-blue }

Tournamnent results [Criterium Senior Vlaams-Brabant 2005-2006 - Serie C Woman](https://competitie.vttl.be/?season=6&menu=7&viewresults=1&t_id=123&s_id=537)

```
C;Criterium Senior Vlaams-Brabant 2005-2006 - Serie C Woman
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;1;505852;505855;3-1
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;2;505256;501243;1-3
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;3;505852;505256;3-0
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;4;505855;505256;1-3
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;5;501243;505852;1-3
T;6;Seniorscriterium Vlaams Brabant;SEN;D;C;;6;501243;505855;3-0
```

## Line "N" : Change in the new ranking of a player

This line allows the modification of the new player's ranking.

Only users who have ```ADMIN``` and ```CLASS``` can use this function.

This line type needs the following extra columns:

### Season
{: .no_toc }

Identifier of the season at the end of which the new ranking will be changed (see also the "I" line ''season'' field).

**Important**: This is not the season in which the new class will be valable (but the previous season).

### Player identifier
{: .no_toc }

Player identifier for whom the new ranking has to be changed. The identifier is a 6 digit number.

### Category
{: .no_toc }

The ranking category for which the new ranking has to be changed. Possible categories are :

- H = Gentlemen
- D = Ladies

### New ranking
{: .no_toc }

The player's new ranking.  Rankings depends on the configuration.

Typical rankings for Table Tennis federation are:

- Gentlemen = NC or NG, E6, E4, E2, E0, D6, D4, D2, D0, C6, C4, C2, C0, B6, B4, B2, B0, A## or As## (where ## is a number).
- Ladies = NC or NG, D6, D4, D2, D0, C6, C4, C2, C0, B6, B4, B2, B0, A## or As## (where ## is a number).

## Line "P" : Change in a player information

_**TODO**_

## Line "L" : Change in a team match schedule

### Season
{: .no_toc }

Identifier of the season when the match is played (see also the same field for _Line "I"_ above).

### Match identifier
{: .no_toc }

Unique identifier of the match for which the date will be changed (see also the same field for _Line "I"_ above).

### Change type
{: .no_toc }

The type of change to proceed:

- **R**: Reset to the official date of the match
- **U**: Update the schedule of the match
- **I**: Invert matches between first and second round

**Important**: if the change type is **U**, additional columns are required

### Change date
{: .no_toc }

If the change type is **U**, this parameter is considered; otherwise it will be ignored.

Indicates the new date of the match.  If left empty, the official date of the match will be used.

Format must be ```YYYY-MM-DD``` where:

- ```YYYY``` is the year on 4 digits,
- ```MM``` is the month on 2 digits (including leading 0 if necessary),
- ```DD``` is the day on 2 digits (including leading 0 if necessary).

### Change time
{: .no_toc }

If the change type is **U**, this parameter is considered; otherwise it will be ignored.

Indicates the new hour of the match.  If left empty, the official hour of the match will be used.

Format must be ```HH-MM``` where:

- ```HH``` is the hour on 2 digits (24 hours format, including leading 0 if necessary),
- ```DD``` is the minute on 2 digits (including leading 0 if necessary).

### Change venue
{: .no_toc }

If the change type is **U**, this parameter is considered; otherwise it will be ignored.

Indicates the new venue of the match.  If left empty, the official venue of the match will be used.

Format must be ```CLUB_ID,VENUE_ID``` where:

- ```CLUB_ID``` is the unique identifier of the club (see field "Home club" for _Line "I"_ above),
- ```VENUE_ID``` is the unique identifier of the club venue (typically 1 when there is only one venue for the club).

Examples
{: .label .label-blue }

Invert matches between Humbeek C and Hurricane C in [division 3A province of Flemish Brabant & Brussels of season 2019-2020](https://competitie.vttl.be/?season=20&div_id=4260&menu=3&type=3&club_id=0)

```
L;20;PVLBH11/019;I
```

Change hour of match Saint-Piat G and Essor Luna Marquain E in [division 5A province of Hainaut of season 2019-2020](https://competitie.vttl.be/?season=20&div_id=4448&menu=3&type=3&club_id=0&province=14)

```
L;20;PVLBH11/019;U;2019-09-28;15:00
```

## Line "F" : Change in fine types definition

With this line type, one can add or change the definition of fine types.  It needs the following columns:

- Season
- Level
- Identifier
- Language
- Description
- Value

The optional following columns can be given:

- Deviations list
- Maximum value
- Order

A fine type is a generic description of a fine that can be assigned to a club.

A fine type is uniquely identified by the combination of the season, the level and its identifier.  If this combination does not exist in the system, a new fine type will be created.  If this combination already exists, the found fine type will be overwritten.

### Season
{: .no_toc }

Identifier of the season for which the fine type must be considered (see also the same field for _Line "I"_ above).

### Level
{: .no_toc }

Identifier of the level for which the fine must be considered.  A level is representing a group of divisons that are managed the same way.

Examples
{: .label .label-blue }

For the 2 main Belgian Table Tennis federations (VTTL & AFTT), the following levels have been defined:

- 6 = Super division
- 1 = National
- 15 = Regional VTTL
- 16 = Regional AFTT
- 4 = Province Hainaut
- 5 = Province Brussel & Vlaams-Brabant
- 7 = Province Oost-Vlaanderen
- 8 = Province Antwerpen
- 9 = Province West-Vlaanderen
- 10 = Province Limburg-Kempen
- 11 = Province Bruxelles & Brabant Wallon
- 12 = Province Namur
- 13 = Province Liège
- 14 = Province Luxembourg

### Identifier
{: .no_toc }

Identifier of the considered fine type.  It is specific to the considered level so it means that several levels can use the same identifier for different fine types.

### Language
{: .no_toc }

The language of the description of the fine type (see next field).

### Description
{: .no_toc }

A description of fine type.

### Value
{: .no_toc }

The value of the fine to be paid by the club when the considered type of fine is assigned to the club.
This is only a default value that can be overwritten when the fine is created.

### Deviations list
{: .no_toc }

The list of deviations that are associated with this fine type.

### Maximum value
{: .no_toc }

If not given:
- an existing fine type will keep its maximum value,
- a new fine type will have no maximum value.

### Order
{: .no_toc }

The display order of this fine type.

If not given:
- an existing fine type will keep its order,
- a new fine type will be given an order that is equal to the maximum order found plus 10.

Examples
{: .label .label-blue }

```
F;21;9;C.18;nl;Opstellen niet gekwalificeerde speler;25;9|18;;1
```

## Line "FD" : Delete fine types

With this line type, one can delete the definition of fine types.  It needs the following columns:

- Season
- Level
- Identifier

A fine type is uniquely identified by the combination of the season, the level and its identifier.  If this combination does not exist in the system, nothing will be done.  If this combination exists, the found fine type will be deleted.

A fine type cannot be deleted if some fines of this fine type have been assigned to a club.

Examples
{: .label .label-blue }

```
F;21;9;C.18
```
