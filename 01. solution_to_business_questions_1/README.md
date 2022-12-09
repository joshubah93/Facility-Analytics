This exercise is designed to explore some typical scenario challenges that faces a facility management business. We are starting from the fundamental statements such as ```SELECT``` , ```WHERE``` , ```ORDER BY``` , ```LIMIT``` and answer questions concerning ```members``` , ```booking``` , ```facilities```.

## 1. How can you retrieve all the information from the cd.facilities table?

```sql
SELECT * 
FROM cd.facilities; 
```

*Output:*

|facid|	name	|       membercost	|guestcost	|initialoutlay	|monthlymaintenance|
|:------------:|:----------:|:----------:|:-----------:|:----------:|:----------------------:|
|0	|Tennis Court 1 	|5|	25	|10000	 |200|
|1	|Tennis Court 2 	|5|	25	|8000	 |200|
|2	|Badminton Court	|0|	15.5	|4000	 |50|
|3	|Table Tennis|	0	|5|	320	|10| 
|4	|Massage Room 1	|35|	80	|4000	|3000|
|5	|Massage Room 2	|35|	80	|4000	|3000|
|6	|Squash Court	|3.5	|17. 5|	5000	|80       | 
|7	|Snooker Table	|0|	5	|450	|15|
|8	|Pool Table	|0	|5|	400	|15|



## 2. You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?

```sql
SELECT name, membercost 
FROM cd.facilities;
```

*Output:*

|name|	membercost|
|:------------:|:----------:|
|Tennis Court 1|	5|
|Tennis Court 2|	5|
|Badminton Court|	0|
|Table Tennis	|0|
|Massage Room 1	|35|
|Massage Room 2	|35|
|Squash Court	|3.5|
|Snooker Table|	0|
|Pool Table|	0|



## 3. How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.


```sql
SELECT facid, name, membercost, monthlymaintenance
FROM cd.facilities
WHERE membercost > 0 
AND (membercost < monthlymaintenance/50.0);
```


*Output:*

|facid	|name|	membercost	|monthlymaintenance|
|:---------:|:--------:|:-----------:|:---------------:|
|4|	Massage Room 1	|35|	3000|
|5|	Massage Room 2	|35|	3000|



## 4. How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.


```sql
SELECT memid, surname, firstname, joindate 
FROM cd.members 
WHERE joindate >= '2012-09-01';
```


*Output:*


|memid	|surname|	firstname|	joindate|
|:--------:|:--------------:|:-----------:|:-----------:|
|24|	Sarwin	|Ramnaresh	|2012-09-01 08:44:42|
|26|	Jones	|Douglas|	2012-09-02 18:43:05|
|27|	Rumney|	Henrietta|	2012-09-05 08:42:35|
|28|	Farrell	|David	|2012-09-15 08:22:05|
|29|	Worthington-Smyth|	Henry|	2012-09-17 12:27:15|
|30|	Purview	|Millicent	|2012-09-18 19:04:01|
|33|	Tupperware	|Hyacinth	|2012-09-18 19:32:05|
|35|	Hunt	|John	|2012-09-19 11:32:45|
|36|	Crumpet	|Erica	2012-09-22 08:36:38|
|37|	Smith	|Darren|	2012-09-26 18:08:45|



## 5. How can you produce an ordered list of the first 10 surnames in the members table? The list must not contain duplicates.

```sql
SELECT DISTINCT surname 
FROM cd.members
ORDER BY surname 
LIMIT 10;
```


*Output:*


|surname|
|:----------:|
|Bader|
|Baker|
|Boothe|
|Butters|
|Coplin|
|Crumpet|
|Dare|
|Farrell|
|Genting|
|GUEST|
