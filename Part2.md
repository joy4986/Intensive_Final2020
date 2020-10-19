_**Instructor Comment: Please provide screenshots of query output next time**_

# 1
```sql
SELECT A.id, A.type, A.status, A.amount, (A.amount - B.avg_amount) AS difference
FROM account A
JOIN (
 SELECT type, AVG(amount) AS avg_amount
 FROM account
 GROUP BY type) B
ON A.type = B.type
WHERE A.status = 'Active';
```

# 2
```sql
CREATE DATABASE problem2;
CREATE EXTERNAL TABLE solution(id INT, fname STRINg, lname STRING, address STRING, city STRING, state STRING, zip STRING, birthday STRING, hireday STRING)
STORED AS PARQUET
LOCATION '/user/training/problem2/data/employee';
```

# 3
```sql
CREATE TABLE solution STORED AS PARQUET AS
SELECT c.id AS id, c.fname AS fname, c.lname AS lname, c.hphone AS hphone 
FROM account AS a JOIN customer AS c ON a.custid=c.id 
WHERE a.amount < 0;
```

# 4
```sql
CREATE DATABASE problem4;
CREATE EXTERNAL TABLE employee1(id int, fname string, lname string, address string, city string, state string, zip string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' 
STORED AS TEXTFILE 
LOCATION '/user/training/problem4/data/employee1';
CREATE EXTERNAL TABLE employee2(id int, none string, fname string, lname string, address string, city string, state string, zip string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
STORED AS TEXTFILE 
LOCATION '/user/training/problem4/data/employee2';
CREATE TABLE problem4.solution 
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' 
STORED AS TEXTFILE 
LOCATION '/user/training/problem4/solution' AS 
SELECT id, initcap(fname) AS fname, INITCAP(lname), address, city, state, zip
FROM employee1
UNION ALL
SELECT id, initcap(fname) AS fname, INITCAP(lname), address, city, state, zip
FROM employee2;
```

# 5
```sql
SELECT fname, lname, city, state
FROM employee
WHERE city='Palo Alto' AND state='CA'
UNION ALL
SELECT fname, lname, city, state
FROM customer
WHERE city='Palo Alto' AND state='CA';
```

# 6
```sql
CREATE TABLE problem6.solution
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' 
STORED AS TEXTFILE AS
SELECT id, fname, lname, address, city, state, zip, SUBSTR(birthday, 0, 5)
FROM employee;
```

# 7
```sql
SELECT concat(fname, ' ', lname) AS name 
FROM employee 
WHERE city='Seattle'
ORDER BY name;
```

# 8
```sql

```

# 9
```sql

```

# 10
```sql
CREATE VIEW solution AS
SELECT C.id AS id
, C.fname AS fname
, C.lname AS lname
, C.city AS city
, C.state AS state
, C.zip AS zip
, B.charge AS charge
, substr(B.tstamp, 0, 10) AS billdate
FROM customer C, billing B
WHERE B.id = C.id
```

# 11
```sql
use default;
select p.name, count(*)
from order_details o, products p
where o.prod_id = p.prod_id
and p.brand = 'Dualcore'
group by p.name
limit 3;
```
