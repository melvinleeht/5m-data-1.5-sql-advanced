# Assignment

## Brief

Write the SQL statements for the following questions.

## Instructions

Paste the answer as SQL in the answer code section below each question.

### Question 1

Using the `claim` and `car` tables, write a SQL query to return a table containing `id, claim_date, travel_time, claim_amt` from `claim`, and `car_type, car_use` from `car`. Use an appropriate join based on the `car_id`.

Answer:

```sql
SELECT claim.id, claim_date, travel_time, claim_amt, car_type, car_use
FROM claim
INNER JOIN car on claim.car_id = car.id;
```

### Question 2

Write a SQL query to compute the running total of the `travel_time` column for each `car_id` in the `claim` table. The resulting table should contain `id, car_id, travel_time, running_total`.

Answer:

```sql
SELECT id, car_id, travel_time, 
SUM (travel_time) OVER (PARTITION BY car_id ORDER BY id ASC, travel_time ASC) AS running_total 
FROM claim;
```

### Question 3

Using a Common Table Expression (CTE), write a SQL query to return a table containing `id, resale_value, car_use` from `car`, where the car resale value is less than the average resale value for the car use.

Answer:

```sql
WITH average_resale_values_by_car_usage AS (
    SELECT car_use, AVG(resale_value) AS average_resale_value 
    FROM car
    GROUP BY car_use
) 
SELECT id, resale_value, c1.car_use
FROM car c1
INNER JOIN average_resale_values_by_car_usage c2
ON c1.car_use = c2.car_use
WHERE c1.resale_value < average_resale_value;
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
