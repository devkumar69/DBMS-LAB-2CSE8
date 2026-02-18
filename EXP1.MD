<div align="center">
  <h1>Experiment 01</h1>
</div>

**Question 1:** Create EMPLOYEE_MASTER table with data from EMPLOYEE table.

```sql
CREATE TABLE EMPLOYEE_MASTER AS
SELECT * FROM EMPLOYEE;
```

**Output:**
```
Query OK, 14 rows affected (0.023 sec)
Records: 14  Duplicates: 0  Warnings: 0
```

```sql
SELECT * FROM EMPLOYEE_MASTER;
```

**Output:**
```
+-------+--------+-----------+------+------------+---------+--------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM   | DEPTNO |
+-------+--------+-----------+------+------------+---------+--------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |   NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 | 300.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |   NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 |1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |   NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |   NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |   NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |   NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |   0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |   NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |   NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |   NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |   NULL |     10 |
+-------+--------+-----------+------+------------+---------+--------+--------+
14 rows in set (0.001 sec)
```

**Question 2:** Delete all records from EMPLOYEE_MASTER where DEPTNO = 10.

```sql
DELETE FROM EMPLOYEE_MASTER
WHERE DEPTNO = 10;
```

**Output:**
```
Query OK, 3 rows affected (0.005 sec)
```

```sql
SELECT * FROM EMPLOYEE_MASTER;
```

**Output:**
```
+-------+--------+-----------+------+------------+---------+--------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM   | DEPTNO |
+-------+--------+-----------+------+------------+---------+--------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |   NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 | 300.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |   NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 |1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |   NULL |     30 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |   NULL |     20 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |   0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |   NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |   NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |   NULL |     20 |
+-------+--------+-----------+------+------------+---------+--------+--------+
11 rows in set (0.001 sec)
```

**Question 3:** Update salary by 10% increase for DEPTNO = 20 in EMPLOYEE_MASTER.

```sql
UPDATE EMPLOYEE_MASTER
SET SAL = SAL * 1.10
WHERE DEPTNO = 20;
```

**Output:**
```
Query OK, 5 rows affected (0.004 sec)
Rows matched: 5  Changed: 5  Warnings: 0
```

```sql
SELECT EMPNO, ENAME, SAL, DEPTNO
FROM EMPLOYEE_MASTER
WHERE DEPTNO = 20;
```

**Output:**
```
+-------+-------+---------+--------+
| EMPNO | ENAME | SAL     | DEPTNO |
+-------+-------+---------+--------+
|  7369 | SMITH |  880.00 |     20 |
|  7566 | JONES | 3272.50 |     20 |
|  7788 | SCOTT | 3300.00 |     20 |
|  7876 | ADAMS | 1210.00 |     20 |
|  7902 | FORD  | 3300.00 |     20 |
+-------+-------+---------+--------+
5 rows in set (0.001 sec)
```

**Question 4:** Alter SAL column to DECIMAL(10,2) in EMPLOYEE_MASTER.

```sql
ALTER TABLE EMPLOYEE_MASTER
MODIFY SAL DECIMAL(10,2);
```

**Output:**
```
Query OK, 11 rows affected (0.031 sec)
Records: 11  Duplicates: 0  Warnings: 0
```

```sql
DESC EMPLOYEE_MASTER;
```

**Output:**
```
+----------+---------------+------+-----+---------+-------+
| Field    | Type          | Null | Key | Default | Extra |
+----------+---------------+------+-----+---------+-------+
| EMPNO    | int(4)        | YES  |     | NULL    |       |
| ENAME    | varchar(10)   | YES  |     | NULL    |       |
| JOB      | varchar(9)    | YES  |     | NULL    |       |
| MGR      | int(4)        | YES  |     | NULL    |       |
| HIREDATE | date          | YES  |     | NULL    |       |
| SAL      | decimal(10,2) | YES  |     | NULL    |       |
| COMM     | decimal(7,2)  | YES  |     | NULL    |       |
| DEPTNO   | int(2)        | YES  |     | NULL    |       |
+----------+---------------+------+-----+---------+-------+
8 rows in set (0.001 sec)
```

**Question 5:** Drop EMPLOYEE_MASTER table.

```sql
DROP TABLE EMPLOYEE_MASTER;
```

**Output:**
```
Query OK, 0 rows affected (0.012 sec)
```

```sql
SHOW TABLES LIKE 'EMPLOYEE_MASTER';
```

**Output:**
```
Empty set (0.001 sec)
```
