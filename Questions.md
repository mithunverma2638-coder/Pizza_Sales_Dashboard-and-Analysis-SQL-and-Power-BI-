Basic:

**Retrieve the total number of orders placed.**

ans--select count(\*) as total\_orders from orders;



**Calculate the total revenue generated from pizza sales.**

ans--select round(sum(order\_details.quantity \* pizzas.price),2) as total\_sales

from order\_details join pizzas

on pizzas.pizza\_id = order\_details.pizza\_id;



**Identify the highest-priced pizza.**

ans--select pizza\_types.name, pizzas.price

from pizza\_types join pizzas

on pizza\_types.pizza\_type\_id =  pizzas.pizza\_type\_id

order by pizzas.price desc limit 1;



**Identify the most common pizza size ordered.**

ans--select pizzas.size, count(order\_details.order\_details\_id) as orders\_count

from pizzas join order\_details

on pizzas.pizza\_id = order\_details.pizza\_id

group by pizzas.size

order by orders\_count desc;



**List the top 5 most ordered pizza types along with their quantities.**

ans--select pizza\_types.name, sum(order\_details.quantity) as quantity

from pizza\_types join pizzas

on pizza\_types.pizza\_type\_id = pizzas.pizza\_type\_id

join order\_details on

order\_details.pizza\_id = pizzas.pizza\_id

group by pizza\_types.name

order by quantity desc

 limit 5;





Intermediate:

**Join the necessary tables to find the total quantity of each pizza category ordered.**

ans-- select pizza\_types.category, sum(order\_details.quantity) as total\_quantity

from pizza\_types join pizzas

on pizza\_types.pizza\_type\_id = pizzas.pizza\_type\_id

join order\_details

on order\_details.pizza\_id = pizzas.pizza\_id

group by pizza\_types.category

order by total\_quantity desc;





**Determine the distribution of orders by hour of the day.**

ans--SELECT

    HOUR(time), COUNT(order\_id) AS order\_count

FROM

    orders

GROUP BY HOUR(time);



Join relevant tables to find the category-wise distribution of pizzas.

ans--select category, count(name) as cate\_name from pizza\_types

group by category;



**Group the orders by date and calculate the average number of pizzas ordered per day.**

ans--SELECT

    ROUND(AVG(total\_quantity), 0) as avg\_ordered\_count

FROM

    (SELECT

        orders.date,

            SUM(order\_details.quantity) AS total\_quantity

    FROM

        orders

    JOIN order\_details ON orders.order\_id = order\_details.order\_id

    GROUP BY orders.date) AS order\_quantity;





**Determine the top 3 most ordered pizza types based on revenue.**

ans-- select pizza\_types.name, sum(order\_details.quantity \* pizzas.price) as revenue

from pizza\_types join pizzas on

pizza\_types.pizza\_type\_id = pizzas.pizza\_type\_id

join order\_details on

order\_details.pizza\_id = pizzas.pizza\_id

group by pizza\_types.name

order by revenue desc

limit 3;





Advanced:

**Calculate the percentage contribution of each pizza type to total revenue.**

ans-- select pizza\_types.category,

(sum(order\_details.quantity\*pizzas.price) / (select round(sum(order\_details.quantity \* pizzas.price),2) as total\_sales

from order\_details join pizzas

on pizzas.pizza\_id = order\_details.pizza\_id) \*100) as revenue

from pizza\_types join pizzas

on pizza\_types.pizza\_type\_id = pizzas.pizza\_type\_id

join order\_details

on order\_details.pizza\_id = pizzas.pizza\_id

group by pizza\_types.category

order by revenue desc;





**Analyze the cumulative revenue generated over time.**

ans-- SELECT

&nbsp;   orders.date,

&nbsp;   SUM(SUM(order\_details.quantity \* pizzas.price)) 

&nbsp;       OVER (ORDER BY orders.date ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cum\_revenue

FROM orders

JOIN order\_details ON orders.order\_id = order\_details.order\_id

JOIN pizzas ON order\_details.pizza\_id = pizzas.pizza\_id

GROUP BY orders.date

ORDER BY orders.date;







**Determine the top 3 most ordered pizza types based on revenue for each pizza category.**

ans-- SELECT name, category, revenue

FROM (

&nbsp;   SELECT 

&nbsp;       category, 

&nbsp;       name, 

&nbsp;       revenue, 

&nbsp;       RANK() OVER (PARTITION BY category ORDER BY revenue DESC) AS rn

&nbsp;   FROM (

&nbsp;       SELECT 

&nbsp;           pizza\_types.category, 

&nbsp;           pizza\_types.name, 

&nbsp;           SUM(order\_details.quantity \* pizzas.price) AS revenue

&nbsp;       FROM pizza\_types

&nbsp;       JOIN pizzas ON pizza\_types.pizza\_type\_id = pizzas.pizza\_type\_id

&nbsp;       JOIN order\_details ON order\_details.pizza\_id = pizzas.pizza\_id

&nbsp;       GROUP BY pizza\_types.category, pizza\_types.name

&nbsp;   ) AS a

) AS b

WHERE rn <= 3;

