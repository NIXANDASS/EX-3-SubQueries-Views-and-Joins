## EX 3 SubQueries, Views and Joins 
#### DATE:
#### Create employee Table
```sql
CREATE TABLE EMP (EMPNO NUMBER(4) PRIMARY KEY,ENAME VARCHAR2(10),JOB VARCHAR2(9),MGR NUMBER(4),HIREDATE DATE,SAL NUMBER(7,2),COMM NUMBER(7,2),DEPTNO NUMBER(2));
```
####Insert the values
```sql
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-80', 800, NULL, 20);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-81', 1600, 300, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-81', 1250, 500, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7566, 'JONES', 'MANAGER', 7839, '02-APR-81', 2975, NULL, 20);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-81', 1250, 1400, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7698, 'BLAKE', 'MANAGER', 7839, '01-MAY-81', 2850, NULL, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7782, 'CLARK', 'MANAGER', 7839, '09-JUN-81', 2450, NULL, 10);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7788, 'SCOTT', 'ANALYST', 7566, '19-APR-87', 3000, NULL, 20);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-81', 5000, NULL, 10);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7844, 'TURNER', 'SALESMAN', 7698, '08-SEP-81', 1500, 0, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7876, 'ADAMS', 'CLERK', 7788, '23-MAY-87', 1100, NULL, 20);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7900, 'JAMES', 'CLERK', 7698, '03-DEC-81', 950, NULL, 30);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7902, 'FORD', 'ANALYST', 7566, TO_DATE('03-DEC-81', 'DD-MON-RR'), 3000, 20, 20);
INSERT INTO EMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
VALUES (7934, 'MILLER', 'CLERK', 7782, TO_DATE('23-JAN-82', 'DD-MON-RR'), 1300, 10, 10);
```

### Create department table
```sql
CREATE TABLE DEPT (DEPTNO NUMBER(2) PRIMARY KEY,DNAME VARCHAR2(14),LOC VARCHAR2(13));
```
#### Insert the values in the department table
```sql
INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (10, 'ACCOUNTING', 'NEW YORK');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (20, 'RESEARCH', 'DALLAS');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (30, 'SALES', 'CHICAGO');

INSERT INTO DEPT (DEPTNO, DNAME, LOC) VALUES (40, 'OPERATIONS', 'BOSTON');
```

#### Q1) List the name of the employees whose salary is greater than that of employee with empno 7566.


#### QUERY:

 ```SELECT ename FROM EMP WHERE sal > (SELECT sal FROM EMP WHERE empno = 7566);```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/b175d634-84c7-404f-b147-398f45e1c3fe)

#### Q2) List the ename,job,sal of the employee who get minimum salary in the company.

#### QUERY:

``` SELECT ename,job,sal FROM EMP WHERE sal = (SELECT MIN(sal) FROM EMP);```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/505fb509-20bc-48a2-bf5b-24d864f3da86)

#### Q3) List ename, job of the employees who work in deptno 10 and his/her job is any one of the job in the department ‘SALES’.

#### QUERY:

 ```SELECT ename,job FROM EMP WHERE deptno = 10 AND job IN (SELECT job FROM EMP WHERE job = 'sales');```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/8a555bb8-55ee-4e50-8aa8-75710393a072)


#### Q4) Create a view empv5 (for the table emp) that contains empno, ename, job of the employees who work in dept 10.

#### QUERY:

```create view empv5 as select EMPNO,ENAME,JOB from EMP where DEPTNO=10;```
```SELECT * FROM empv5; ```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/f820889d-5c50-4584-b7ce-cc79fa8324a0)


#### Q5) Create a view with column aliases empv30 that contains empno, ename, sal of the employees who work in dept 30. Also display the contents of the view.

#### QUERY:

```create view empv30 AS select EMPNO,ENAME,SAL from EMP where DEPTNO=30;```
```SELECT * FROM empv30;```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/65208105-0e64-4358-b5b2-9144b6d3071f)


#### Q6) Update the view empv5 by increasing 10% salary of the employees who work as ‘CLERK’. Also confirm the modifications in emp table

#### QUERY:
 ```create view empv6 as select EMPNO,ENAME,SAL,JOB from EMP;```
 ```SELECT * FROM empv6;```
#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/66920e40-4ae8-478b-9e1b-c32b4fb7bb05)

## Create a Customer1 Table
```sql
CREATE TABLE Customer1 (customer_id INT,cust_name VARCHAR(20),city VARCHAR(20),grade INT,salesman_id INT);
```
## Inserting Values to the Table
```sql
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3002, 'Nick Rimando', 'New York', 100, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3007, 'Brad Davis', 'New York', 200, 5001);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3005, 'Graham Zusi', 'California', 200, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3008, 'Julian Green', 'London', 300, 5002);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3004, 'Fabian Johnson', 'Paris', 300, 5006);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3009, 'Geoff Cameron', 'Berlin', 100, 5003);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
INSERT INTO Customer1 (customer_id, cust_name, city, grade, salesman_id) VALUES(3001, 'Brad Guzan', 'London', NULL, 5005);
```
## Create a Salesperson1 table
```sql
CREATE TABLE Salesman1 (salesman_id INT,name VARCHAR(20),city VARCHAR(20),commission DECIMAL(4,2));
```
## Inserting Values to the Table
```sql
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5001, 'James Hoog', 'New York', 0.15);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5002, 'Nail Knite', 'Paris', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5005, 'Pit Alex', 'London', 0.11);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5006, 'Mc Lyon', 'Paris', 0.14);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5007, 'Paul Adam', 'Rome', 0.13);
INSERT INTO Salesman1 (salesman_id, name, city, commission) VALUES(5003, 'Lauson Hen', 'San Jose', 0.12);
```
#### Q7) Write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

#### QUERY:
```select s.name,c.cust_name,s.city from salesman1 s ,customer1 c where s.city=c.city;```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/10bb6a16-011f-426c-a88c-a8715cf30fc4)


#### Q8) Write a SQL query to find salespeople who received commissions of more than 13 percent from the company. Return Customer Name, customer city, Salesman, commission.


#### QUERY:

```select s.name,c.cust_name,c.city,s.commission from salesman1 s inner join customer1 c on s.city=c.city where s.commission>0.13;```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/5c9e0b6c-292d-457d-ae4d-be60e67bce32)

#### Q9) Perform Natural join on both tables

#### QUERY:
``` select * from salesman1 s natural join customer1 c;```

#### OUTPUT:
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/5dbdfa7e-eef8-4b09-b7b3-8bde54734063)

#### Q10) Perform Left and right join on both tables

#### QUERY:
```
select s.name,c.cust_name,c.city,s.commission from salesman1 s left join customer1 c on s.salesman_id=c.salesman_id;
select s.name,c.cust_name,c.city,s.commission from salesman1 s right join customer1 c on s.salesman_id=c.salesman_id;
```
#### OUTPUT:

#### LEFT JOIN
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/78608ba5-033b-4cc6-93b3-ec72c7d8add0)

#### RIGHT JOIN
![image](https://github.com/NIXANDASS/EX-3-SubQueries-Views-and-Joins/assets/118781418/06988161-45ab-4e50-a1eb-e0247227a7fb)
#### RESULT:
The given sql queries were executed
