# northwind.db Problems Solutions

You can use the Entity Relationship Diagram (ERD) to determine what data to store, the entities, their attributes, and how entities relate to other entities.

![northwind_ERD](https://github.com/user-attachments/assets/db5d5ea3-d259-46fa-b629-e1a743f50825)

## Solutions
### Level - EASY
#### Questions: 1 - 9
1. Show the category_name and description from the categories table sorted by category_name.
```SQL
SELECT category_name, description FROM categories
order by category_name;
```
2. Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'
```SQL
SELECT contact_name, address, city FROM customers
WHERE country NOT IN ('Germany','Mexico','Spain');
```
3. Show order_date, shipped_date, customer_id, Freight of all orders placed on 2018 Feb 26
```SQL
SELECT order_date, shipped_date, customer_id, freight 
from orders
WHERE order_date = '2018-02-26';
```
4. Show the employee_id, order_id, customer_id, required_date, shipped_date from all orders shipped later than the required date
```SQL
SELECT employee_id, order_id, customer_id, required_date, shipped_date
FROM orders
where shipped_date > required_date;
```
5. Show all the even numbered Order_id from the orders table
```SQl
SELECT order_id FROM orders
where MOD(order_id,2) = 0;
```
6. Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name
```SQL
SELECT city, company_name, contact_name FROM customers
where city LIKE '%L%'
order by contact_name;
```
7. Show the company_name, contact_name, fax number of all customers that has a fax number. (not null)
```SQL
SELECT company_name, contact_name, fax FROM customers
where fax not NULL;
```
8. Show the first_name, last_name. hire_date of the most recently hired employee.
```SQL
SELECT first_name, last_name, MAX(hire_date) FROM employees;
```
9. Show the average unit price rounded to 2 decimal places, the total units in stock, total discontinued products from the products table.
```SQL
SELECT ROUND(avg(unit_price),2) AS average_price, 
sum(units_in_stock) AS total_stock, 
SUM(discontinued) AS total_discontinued FROM products;
```

### Level - MEDIUM
#### Questions: 1 - 9
1. Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table
```SQL
SELECT p.product_name, s.company_name, c.category_name
FROM products p
JOIN suppliers s ON s.supplier_id = p.Supplier_id
JOIN categories c On c.category_id = p.Category_id;
```
2. Show the category_name and the average product unit price for each category rounded to 2 decimal places.
```SQL
SELECT c.category_name, round(avg(p.unit_price),2) as average_unit_price
FROM products p
JOIN categories c On c.category_id = p.Category_id
GROUP BY c.category_name
```
3. Show the city, company_name, contact_name from the customers and suppliers table merged together.
Create a column which contains 'customers' or 'suppliers' depending on the table it came from.
```SQL
select City, company_name, contact_name, 'customers' as relationship 
from customers
union
select city, company_name, contact_name, 'suppliers'
from suppliers
```
4. Show the total amount of orders for each year/month.
```SQL
SELECT year(order_date) AS order_year, month(order_date) AS order_month,
count(*) AS no_of_orders FROM orders
group by order_year, order_month;
```





































































































































