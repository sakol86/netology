# Домашнее задание к занятию 12.4. «SQL. Часть 2» - Ковбаса Анна

---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```sql
SELECT CONCAT_WS(' ', s2.first_name, s2.last_name) AS staff, c.city, COUNT(c2.customer_id) as customers
FROM sakila.store s 
JOIN sakila.address a ON a.address_id = s.address_id 
JOIN sakila.city c ON c.city_id = a.city_id 
JOIN sakila.staff s2 ON s2.store_id = s.store_id 
JOIN sakila.customer c2 ON c2.store_id = s.store_id 
GROUP BY s.store_id, s2.staff_id 
HAVING COUNT(c2.customer_id) > 300 ;
```

![1-1](https://github.com/kovbasaad/12-4-homework/blob/main/img%20(2)/1-1.JPG)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql
SELECT COUNT(1) 
FROM sakila.film 
WHERE length > (SELECT AVG(length) FROM sakila.film);
```

![2-1](https://github.com/kovbasaad/12-4-homework/blob/main/img%20(2)/2-1.JPG)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```sql
SELECT MONTH (payment_date), SUM(amount), COUNT(rental_id) 
FROM sakila.payment 
GROUP BY MONTH (payment_date)
HAVING SUM(amount) >= ALL (
SELECT SUM(amount)
FROM sakila.payment 
GROUP BY MONTH (payment_date));
```
```sql
SELECT MONTH (payment_date), SUM(amount), COUNT(rental_id) 
FROM sakila.payment 
GROUP BY MONTH (payment_date)
ORDER BY SUM(amount) DESC 
LIMIT 1;
```

![3-1](https://github.com/kovbasaad/12-4-homework/blob/main/img%20(2)/3-1.JPG)
