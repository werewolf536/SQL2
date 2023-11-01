# Домашнее задание к занятию «SQL. Часть 2» - Стрельцов Владимир

Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.
```
SELECT CONCAT(sta.first_name,' ', sta.last_name) AS 'Name Staff', ci.city AS City, COUNT(customer_id) AS 'Total customer'
from customer co
join store st on st.store_id = co.store_id
join staff sta on sta.store_id = st.store_id 
join address ad on ad.address_id = sta.address_id 
join city ci on ci.city_id = ad.city_id 
group by st.store_id, ci.city, sta.first_name, sta.last_name 
having COUNT(customer_id)>300; 
```

![img](/img/2023-11-01_15-15-22.png)


## Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.


```select COUNT(film_id) from film WHERE length > (select AVG(length) from film);```

![img](/img/2023-11-01_15-39-14.png)


## Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
```
SELECT MONTH(payment_date) AS Month, SUM(amount) AS Amount, COUNT(payment_id) AS Payments  
from payment p 
group by MONTH(payment_date)
ORDER  BY COUNT(payment_id) DESC limit 1;
```
![img](/img/2023-11-01_15-33-40.png)
