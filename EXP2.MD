<div align="center">
  <h1>Experiment 02</h1>
</div>

**Perform Following Queries using Employee Table (Retrieving Data)**

---

**Query 1:** List all distinct jobs in Employee.

```sql
SELECT DISTINCT JOB FROM EMPLOYEE;
```

**Output:**
```
+-----------+
| JOB       |
+-----------+
| CLERK     |
| SALESMAN  |
| MANAGER   |
| ANALYST   |
| PRESIDENT |
+-----------+
5 rows in set (0.001 sec)
```

---

**Query 2:** List all information about employee in Department Number 30.

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 30;
```

**Output:**
```
+-------+--------+----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+----------+------+------------+---------+---------+--------+
|  7499 | ALLEN  | SALESMAN | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN | 7698 | 1981-02-22 | 1250.00 |  300.00 |     30 |
|  7654 | MARTIN | SALESMAN | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
+-------+--------+----------+------+------------+---------+---------+--------+
6 rows in set (0.001 sec)
```

---

**Query 3:** Find all department numbers with department number greater than 20.

```sql
SELECT DISTINCT DEPTNO FROM EMPLOYEE
WHERE DEPTNO > 20;
```

**Output:**
```
+--------+
| DEPTNO |
+--------+
|     30 |
+--------+
1 row in set (0.001 sec)
```

---

**Query 4:** Find all information about all the managers as well as the clerks in department 30.

```sql
SELECT * FROM EMPLOYEE
WHERE (JOB = 'MANAGER' OR JOB = 'CLERK')
AND DEPTNO = 30;
```

**Output:**
```
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7698 | BLAKE | MANAGER | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
+-------+-------+---------+------+------------+---------+------+--------+
2 rows in set (0.001 sec)
```

---

**Query 5:** List the Employee name, Employee numbers and department of all clerks.

```sql
SELECT ENAME, EMPNO, DEPTNO FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

**Output:**
```
+--------+-------+--------+
| ENAME  | EMPNO | DEPTNO |
+--------+-------+--------+
| SMITH  |  7369 |     20 |
| ADAMS  |  7876 |     20 |
| JAMES  |  7900 |     30 |
| MILLER |  7934 |     10 |
+--------+-------+--------+
4 rows in set (0.001 sec)
```

---

**Query 6:** Find all managers not in department 30.

```sql
SELECT * FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND DEPTNO != 30;
```

**Output:**
```
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7566 | JONES | MANAGER | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7782 | CLARK | MANAGER | 7839 | 1981-06-09 | 2450.00 | NULL |     10 |
+-------+-------+---------+------+------------+---------+------+--------+
2 rows in set (0.001 sec)
```

---

**Query 7:** List information about all Employees in department 10 who are not manager or clerks.

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

**Output:**
```
+-------+-------+-----------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB       | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+-----------+------+------------+---------+------+--------+
|  7839 | KING  | PRESIDENT | NULL | 1981-11-17 | 5000.00 | NULL |     10 |
+-------+-------+-----------+------+------------+---------+------+--------+
1 row in set (0.001 sec)
```

---

**Query 8:** Find Employees and jobs earning between 1200 and 1400.

```sql
SELECT ENAME, JOB, SAL FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;
```

**Output:**
```
+--------+----------+---------+
| ENAME  | JOB      | SAL     |
+--------+----------+---------+
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
| MILLER | CLERK    | 1300.00 |
+--------+----------+---------+
3 rows in set (0.001 sec)
```

---

**Query 9:** List Name and Department Number of employee who are clerks, analyst or salesman.

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| SMITH  |     20 |
| ALLEN  |     30 |
| WARD   |     30 |
| MARTIN |     30 |
| SCOTT  |     20 |
| TURNER |     30 |
| ADAMS  |     20 |
| JAMES  |     30 |
| FORD   |     20 |
| MILLER |     10 |
+--------+--------+
10 rows in set (0.001 sec)
```

---

**Query 10:** List Name and Department Number of employee whose names began with M.

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE ENAME LIKE 'M%';
```

**Output:**
```
+--------+--------+
| ENAME  | DEPTNO |
+--------+--------+
| MARTIN |     30 |
| MILLER |     10 |
+--------+--------+
2 rows in set (0.001 sec)
```
