In this second part of the exercise, we will go a step futher to explore the use of aggregate statements such ```GROUP BY``` , ```HAVING```  and  ```JOIN``` statement to solve challenges.


## 6. You'd like to get the signup date of your last member. How can you retrieve this information?

```sql
SELECT 
MAX(joindate) 
AS latest_signup 
FROM cd.members;
```

*Output:*

|Latest_signup|
|:----------------:|
|2012-09-26 18:08:45|


## 7. Produce a count of the number of facilities that have a cost to guests of 10 or more.

```sql
SELECT COUNT(*) 
FROM cd.facilities 
WHERE guestcost >= 10;
```

*Output:*

|count|
|:------:|
|6|



## 8. Produce a list of the total number of slots booked per facility in the month of September 2012. Produce an output table consisting of facility id and slots, sorted by the number of slots.

```sql
SELECT facid, sum(slots) 
AS Total Slots 
FROM cd.bookings 
WHERE starttime >= '2012-09-01' 
AND starttime < '2012-10-01' 
GROUP BY facid ORDER BY SUM(slots);
```

*Output:*


|facid	|Total Slots|
|:----------:|:----------:|
|5	|122|
|3	|422|
|7	|426|
|8	|471|
|6	|540|
|2	|570|
|1|	588|
|0|	591|
|4|	648|



## 10. Produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and total slots, sorted by facility id.

```sql
SELECT facid, sum(slots) 
AS total_slots 
FROM cd.bookings
 GROUP BY facid 
HAVING SUM(slots) > 1000 
ORDER BY facid;
```

*Output:*


|facid	|total_slots|
|:------:|:-------:|
|0	|1320|
|1	|1278|
|2	|1209|
|4	|1404|
|6	|1104|


## 11. How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.


```sql
SELECT cd.bookings.starttime AS start, cd.facilities.name 
AS name 
FROM cd.facilities 
INNER JOIN cd.bookings
ON cd.facilities.facid = cd.bookings.facid 
WHERE cd.facilities.facid IN (0,1) 
AND cd.bookings.starttime >= '2012-09-21' 
AND cd.bookings.starttime < '2012-09-22' 
ORDER BY cd.bookings.starttime;
```


*Output:*


|start	|name|
|:------:|:-------:|
|2012-09-21 08:00:00	|Tennis Court 1|
|2012-09-21 08:00:00	|Tennis Court 2|
|2012-09-21 09:30:00	|Tennis Court 1|
|2012-09-21 10:00:00	|Tennis Court 2|
|2012-09-21 11:30:00	|Tennis Court 2|
|2012-09-21 12:00:00	|Tennis Court 1|
|2012-09-21 13:30:00	|Tennis Court 1|
|2012-09-21 14:00:00	|Tennis Court 2|
|2012-09-21 15:30:00	|Tennis Court 1|
|2012-09-21 16:00:00	|Tennis Court 2|
|2012-09-21 17:00:00	|Tennis Court 1|
|2012-09-21 18:00:00	|Tennis Court 2|



## 12. How can you produce a list of the start times for bookings by members named 'David Farrell'?


```sql
SELECT cd.bookings.starttime 
FROM cd.bookings 
INNER JOIN cd.members ON 
cd.members.memid = cd.bookings.memid 
WHERE cd.members.firstname='David' 
AND cd.members.surname='Farrell';
```


*Output:*

|Starttime|
|:----------:|
|2012-09-18 09:00:00|
|2012-09-18 13:30:00|
|2012-09-18 17:30:00|
|2012-09-18 20:00:00|
|2012-09-19 09:30:00|
|2012-09-19 12:00:00|
|2012-09-19 15:00:00|
|2012-09-20 11:30:00|
|2012-09-20 14:00:00|
|2012-09-20 15:30:00|
