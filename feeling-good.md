- `Question 01`: Query for hotels that allow pets
```sql
SELECT * FROM hotels
WHERE pets IS TRUE;
```

- `Question 02`: Query for hotels that allow pets AND have vacancies
```sql
SELECT hotels.name, hotels.city, hotels.state, COUNT(hotels.name) AS rooms
FROM hotels INNER JOIN rooms
ON rooms.hotel_id = hotels.id
WHERE hotels.pets IS TRUE AND rooms.vacant IS TRUE
GROUP BY hotels.name, hotels.city, hotels.state;
```

- `Question 03`: Query for the average room price for a hotel that allows pets
```sql
SELECT hotels.name, AVG(rooms.price)
FROM hotels JOIN rooms
ON rooms.hotel_id = hotels.id
WHERE hotels.pets IS TRUE
GROUP BY hotels.name;
```

- `Question 04`: Query for the most expensive room
```sql
SELECT hotels.name as hotel_name, rooms.name as room_name,  max(rooms.price) AS price
FROM hotels JOIN rooms
ON rooms.hotel_id = hotels.id 
WHERE rooms.price IS NOT null
GROUP BY hotels.name, rooms.name
ORDER BY price DESC
LIMIT 1;
```

- `Question 05`: Query for the average price of a room that has a name that includes **queen** in it (case insensitive)
```sql
SELECT AVG(price)
FROM (
	SELECT hotels.name as hotel_name, rooms.name as room_name, rooms.price as price
	FROM hotels JOIN rooms
	ON rooms.hotel_id = hotels.id
	WHERE rooms.name ILIKE '%queen%'
);
```

- `Question 06`: Update a room at Hotel California with room number 202 from vacant-true to vacant-false.
```sql
UPDATE rooms
SET vacant = FALSE
WHERE id = (
    SELECT rooms.id
    FROM hotels JOIN rooms
    ON rooms.hotel_id = hotels.id
    WHERE hotels.name = 'Hotel California' AND rooms.room_num = 202
    );

```

- `Question 07`: Update all the rooms with the hotel_id of 7 to have now a hotel_id that matches the Grand Budapest Hotel
```sql
UPDATE rooms
SET hotel_id = (SELECT id
				FROM hotels
				WHERE name = 'Grand Budapest Hotel')
WHERE hotel_id = 7
RETURNING *;
```





