# Level-02-Assignment-03
## Vehicle Rental System - Database Design & SQL Queries

Query 1: JOIN
Retrieve booking information along with:

Customer name

Vehicle name

Concepts used: INNER JOIN

```sql
SELECT
    u.name AS customer_name,
    v.name AS vehicle_name,
    b.starting_date AS start_date,
    b.ending_date AS end_date,
    b.status
FROM
    booking b
    INNER JOIN users u ON b.user_id = u.user_id
    INNER JOIN vehicles v ON b.vehicle_id = v.vehicle_id;
```
Query 2: EXISTS

Find all vehicles that have never been booked.

Concepts used: NOT EXISTS

```sql
SELECT
    v.vehicle_id,
    v.name,
    v.type,
    v.model,
    v.regi_id AS registration_number,
    v.price_per_day AS rental_price,
    v.status
FROM
    vehicles v
WHERE
    NOT EXISTS (
        SELECT 1
        FROM booking b
        WHERE b.vehicle_id = v.vehicle_id
    );
```
Query 3: WHERE

Retrieve all available vehicles of a specific type (e.g. cars).

Concepts used: SELECT, WHERE

```sql
SELECT
    v.vehicle_id,
    v.name,
    v.type,
    v.model,
    v.regi_id AS registration_number,
    v.price_per_day AS rental_price,
    v.status
FROM
    vehicles v
WHERE
    v.status = 'available'
    AND v.type = 'car';
```
Query 4: GROUP BY and HAVING

Find the total number of bookings for each vehicle and display only those vehicles that have more than 2 bookings.

Concepts used: GROUP BY, HAVING, COUNT

```sql
SELECT
    v.name AS vehicle_name,
    COUNT(v.vehicle_id) AS booking_count
FROM
    booking b
    JOIN vehicles v ON b.vehicle_id = v.vehicle_id
GROUP BY
    v.name,
    v.vehicle_id
HAVING
    COUNT(v.vehicle_id) > 2;
```

[video](https://youtu.be/qxmKsMjRl3g?si=U8YsuWV874EpBcXP)
