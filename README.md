#Duplicates
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

# Missing Values – there weren’t any based on the categories below. To add the missing values, I would use the AVG value.
SELECT * FROM film
WHERE rental_rate  IS NULL

SELECT * FROM film
WHERE film_id IS NULL

SELECT * FROM customer
WHERE email IS NULL

SELECT * FROM customer
WHERE customer_id IS NULL
GIT HUB SQL SECTION


# Non-Uniform data – no data found based on the queries below. But if there were, I would use UPDATE table, SET column = ‘value’, WHERE column IN (‘values’)
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

# Summarizing Data
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

#Top 10 countries for Rockbuster in terms of customer numbers, limited output to 10
SELECT country, COUNT (customer_id) 
FROM country
JOIN city
ON country.country_id = city.country_id
JOIN address
ON city.city_id = address.city_id
JOIN customer
ON customer.address_id = address.address_id
GROUP BY country
ORDER BY COUNT (customer_id) DESC
LIMIT 10

#Top 10 cities within the top 10 countries 
SELECT country.country AS “Country”, city.city AS “City”, COUNT (customer.customer_id) as "No_Customer"  
FROM country
JOIN city
ON country.country_id = city.country_id
JOIN address
ON city.city_id = address.city_id
JOIN customer
ON customer.address_id = address.address_id
WHERE country.country in ('India', 'China', 'United States', 'Japan', 'Brazil', 'RussianFederation', 'Philippines', 'Turkey', 'Indonesia')
GROUP BY country.country, city.city
ORDER BY "No_Customer" DESC
LIMIT 10

#Top 5 customers in the top 10 cities who have paid the highest total amounts to Rockbuster
select payment.customer_id as "Customer_ID", customer.first_name as "First_Name", customer.last_name as "Last_Name", Country.country as "Country", city.city as "City", 
sum (payment.amount) as "Total Amount Paid" from country
join city
on country.country_id = city.country_id
join address
on city.city_id = address.city_id
join customer
on customer.address_id = address.address_id
join payment
on payment.customer_id = customer.customer_id
where city.city in ('Saint-Denis', 'Cape Coral', 'Santa Brbara dOeste', 'Apeldoorn', 'Molodetno', 'Qomsheh', 'London', 'Memphis', 'Richmond Hill', 'Tanza')
group by city.city, payment.customer_id, customer.first_name, customer.last_name, Country.country, payment.amount
order by "Total Amount Paid" DESC
limit 10

