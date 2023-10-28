# Ödev 12
### Aşağıdaki sorgu senaryolarını dvdrental örnek veri tabanı üzerinden gerçekleştiriniz.

- film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
```
SELECT COUNT(*) FROM film
WHERE length> 
(
	SELECT AVG(length) 
	FROM film
);
```
- film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?
```
SELECT COUNT(*) FROM film
WHERE rental_rate = 
(
 SELECT MAX(rental_rate) FROM film
);

```
- film tablosunda en düşük rental_rate ve en düşük replacement_cost değerlerine sahip filmleri sıralayınız.
```
SELECT title,rental_rate,replacement_cost FROM film
WHERE (rental_rate, replacement_cost) = ANY 
(
	SELECT MIN(rental_rate),MIN(replacement_cost) FROM film
);
```
- payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
```
SELECT COUNT(payment.customer_id) AS Purchases, customer.first_name, customer.last_name FROM payment
INNER JOIN customer ON payment.customer_id=customer.customer_id
GROUP BY payment.customer_id,customer.first_name,customer.last_name
ORDER BY COUNT(payment.customer_id) DESC
LIMIT 5;
```