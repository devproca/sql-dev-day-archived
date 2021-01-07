# sql-dev-day

## Install Docker

Download and install docker

```
https://hub.docker.com/editions/community/docker-ce-desktop-mac?tab=description
```

## Install MySQLWorkBench

Download and install MySQLWorkBench

Note you will need to right click and select open when it tells you "can’t be opened because Apple cannot check it for malicious software."


```
https://www.mysql.com/products/workbench/
```

## Launch Docker Image

```
docker-compose -f dockerImage.yaml up
```

## Connect to Docker Image in MySQLWorkBench
Hostname: 127.0.0.1
Port: 3306
user: root 
password: password


## Import database MySQLWorkBench

Server -> Data Import -> Import from self contained file -> devDay.sql


## Data Structures

Users
id (PK,Int)
firstname(String)
lastname(String)
username(String)

Phonnumbers
user_id(Fk,Int)
phonenumber(String)

Emails
user_id(Fk,Int)
email(String)

Product
id(PK,Int)
name(String)
price(Double)
category(Int)
created_at(Date)

Orders
id(Pk,Int)
user_id(Fk,Int)
product_id(Fk,Int)
purchase_date(Date)

## sql with (common table expressions)
A Common Table Expression (CTE) is the result set of a query which exists temporarily and for use only within the context of a larger query.

Syntax

```
SELECT t1.data1,t2.data2 FROM Table1 as t1 JOIN Table2 as t2 ON 
Table1.someKey = Table2.someKey
```


## Joins (inner,left,right)
Joins are used to query related data from different tables.

Syntax

```
SELECT Table1.data1,Table2.data2 FROM Table1 JOIN Table2 ON 
Table1.someKey = Table2.someKey
```

Inner Join

Inner Join willl only show rows that match from both tables

Left Join

Left Join will show all matching rows from the 'left' (first) table and null for the non matching from the 'right' (second) table

Right Join

Right Join does the opposite of Left Join and will return null on the 'left' (first) table and all matching rows on the 'right' (second) table

### Exercise 2-a
Query Users and there email addresses using a left and inner join
use the 'users' table as the left table and 'emails' as the right

### Exercise 2-b
Query Users and there email addresses using a left and inner join
use the 'emails' table as the left table and 'users' as the right


## Analytic functions (window functions)



Syntax

```
SELECT data1, data2, aggregate_function(data3)
FROM table
```

Aggregate Functions
AVG()
COUNT()
COUNT(DISTINCT)
MAX()
MIN()
SUM()


### Exercise 3-a
Create a query to get the total price of all the products

```
SELECT SUM(p.price) as total_price
From  products p;
```



## Group by

GROUP BY returns one row for each group. In other words, it reduces the number of rows in the result set. It is usually used with an aggregate function

Syntax

```
SELECT data1, data2, aggregate_function(data3)
FROM table
GROUP BY data1
```

### Exercise 4-a

Create a query that shows who has the most orders


Answer 
```
SELECT u.firstname, COUNT(*) as num_orders FROM users u
left join orders o on u.id = o.user_id
group by u.firstname
order by num_orders desc;
```


### Exercise 4-b
create a query that shows the total purchase order of ever user

```
SELECT u.firstname, SUM(p.price) as total_purchase 
From users u, products p 
join orders o on p.id
where u.id = o.user_id
group by u.firstname;
```












