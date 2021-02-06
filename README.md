# SQL
##If there were duplicates, I would clean the data as follows: I would create a view with unique records. I would be shy about deleting at this point.
SELECT title,
       release_year,
       language_id,
       rental_duration,
       COUNT(*)
FROM film
GROUP BY title,
         release_year,
         language_id,
         rental_duration
HAVING COUNT(*) >1; --no result set means we have no duplicates

SELECT customer_id,
       store_id,
       first_name,
       last_name,
	   email,
	   address_id,
       COUNT(*)
FROM customer
GROUP BY customer_id,
       store_id,
       first_name,
       last_name,
	   email,
	   address_id
HAVING COUNT(*) >1; --no result set means we have no duplicates
SELECT 

## Missing Values – there weren’t any based on the categories below. To add the missing values, I would use the AVG value.
SELECT * FROM film
WHERE rental_rate  IS NULL

SELECT * FROM film
WHERE film_id IS NULL

SELECT * FROM customer
WHERE email IS NULL

SELECT * FROM customer
WHERE customer_id IS NULL
GIT HUB SQL SECTION


## Non-Uniform data – no data found based on the queries below. But if there were, I would use UPDATE table, SET column = ‘value’, WHERE column IN (‘values’)
SELECT store_id
FROM customer
GROUP BY store_id

SELECT DISTINCT email
FROM customer
GROUP BY email

SELECT title
FROM film
GROUP BY title

SELECT DISTINCT film_id
FROM film
GROUP by film_id

## Summarizing Data
SELECT MIN(rental_duration) AS min_dur,
      MAX (rental_duration) AS max_dur,
      AVG(rental_duration) AS avg_dur,
      COUNT(rental_duration) AS count_rent_dur_values,
      COUNT(*) AS count_rows
FROM film;

SELECT mode()
WITHIN GROUP (ORDER BY activebool)
FROM customer;

SELECT mode()
WITHING GROUP (ORDER BY store_id)
FROM customer;
