<div align="center">
  <h1>Experiment 03</h1>
</div>

**Perform Following Queries using Employee Table (Retrieving Data)**

---

**Query 1:** List all employees and jobs in Department 30 in descending order by salary.

```sql
SELECT ENAME, JOB, SAL FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

**Output:**
```
+--------+----------+---------+
| ENAME  | JOB      | SAL     |
+--------+----------+---------+
| BLAKE  | MANAGER  | 2850.00 |
| ALLEN  | SALESMAN | 1600.00 |
| TURNER | SALESMAN | 1500.00 |
| WARD   | SALESMAN | 1250.00 |
| MARTIN | SALESMAN | 1250.00 |
| JAMES  | CLERK    |  950.00 |
+--------+----------+---------+
6 rows in set (0.001 sec)
```

---

**Query 2:** List job and Department Number of employees whose name are five letters long, begin with "A" and end with "N".

```sql
SELECT ENAME, JOB, DEPTNO FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

**Output:**
```
+-------+----------+--------+
| ENAME | JOB      | DEPTNO |
+-------+----------+--------+
| ALLEN | SALESMAN |     30 |
+-------+----------+--------+
1 row in set (0.001 sec)
```

---

**Query 3:** Display the name of employees whose name starts with alphabet S.

```sql
SELECT ENAME FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| SCOTT |
+-------+
2 rows in set (0.001 sec)
```

---

**Query 4:** Display the names of employees whose name ends with alphabet S.

```sql
SELECT ENAME FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

**Output:**
```
+-------+
| ENAME |
+-------+
| JONES |
| ADAMS |
| JAMES |
+-------+
3 rows in set (0.001 sec)
```

---

**Query 5:** Display the names of employees working in department number 10 or 20 or 40 or employees working as clerks, salesman or analyst.

```sql
SELECT ENAME, JOB, DEPTNO FROM EMPLOYEE
WHERE DEPTNO IN (10, 20, 40)
OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
```

**Output:**
```
+--------+-----------+--------+
| ENAME  | JOB       | DEPTNO |
+--------+-----------+--------+
| SMITH  | CLERK     |     20 |
| ALLEN  | SALESMAN  |     30 |
| WARD   | SALESMAN  |     30 |
| JONES  | MANAGER   |     20 |
| MARTIN | SALESMAN  |     30 |
| CLARK  | MANAGER   |     10 |
| SCOTT  | ANALYST   |     20 |
| KING   | PRESIDENT |     10 |
| TURNER | SALESMAN  |     30 |
| ADAMS  | CLERK     |     20 |
| JAMES  | CLERK     |     30 |
| FORD   | ANALYST   |     20 |
| MILLER | CLERK     |     10 |
+--------+-----------+--------+
13 rows in set (0.001 sec)
```

---

**Query 6:** Display employee number and names for employees who earn commission.

```sql
SELECT EMPNO, ENAME, COMM FROM EMPLOYEE
WHERE COMM IS NOT NULL AND COMM > 0;
```

**Output:**
```
+-------+--------+---------+
| EMPNO | ENAME  | COMM    |
+-------+--------+---------+
|  7499 | ALLEN  |  300.00 |
|  7521 | WARD   |  300.00 |
|  7654 | MARTIN | 1400.00 |
+-------+--------+---------+
3 rows in set (0.001 sec)
```

---

**Query 7:** Display employee number and total salary for each employee.

```sql
SELECT EMPNO, ENAME, SAL + IFNULL(COMM, 0) AS TOTAL_SAL
FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+-----------+
| EMPNO | ENAME  | TOTAL_SAL |
+-------+--------+-----------+
|  7369 | SMITH  |    800.00 |
|  7499 | ALLEN  |   1900.00 |
|  7521 | WARD   |   1550.00 |
|  7566 | JONES  |   2975.00 |
|  7654 | MARTIN |   2650.00 |
|  7698 | BLAKE  |   2850.00 |
|  7782 | CLARK  |   2450.00 |
|  7788 | SCOTT  |   3000.00 |
|  7839 | KING   |   5000.00 |
|  7844 | TURNER |   1500.00 |
|  7876 | ADAMS  |   1100.00 |
|  7900 | JAMES  |    950.00 |
|  7902 | FORD   |   3000.00 |
|  7934 | MILLER |   1300.00 |
+-------+--------+-----------+
14 rows in set (0.001 sec)
```

---

**Query 8:** Display employee number and annual salary for each employee.

```sql
SELECT EMPNO, ENAME, SAL * 12 AS ANNUAL_SAL
FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+------------+
| EMPNO | ENAME  | ANNUAL_SAL |
+-------+--------+------------+
|  7369 | SMITH  |    9600.00 |
|  7499 | ALLEN  |   19200.00 |
|  7521 | WARD   |   15000.00 |
|  7566 | JONES  |   35700.00 |
|  7654 | MARTIN |   15000.00 |
|  7698 | BLAKE  |   34200.00 |
|  7782 | CLARK  |   29400.00 |
|  7788 | SCOTT  |   36000.00 |
|  7839 | KING   |   60000.00 |
|  7844 | TURNER |   18000.00 |
|  7876 | ADAMS  |   13200.00 |
|  7900 | JAMES  |   11400.00 |
|  7902 | FORD   |   36000.00 |
|  7934 | MILLER |   15600.00 |
+-------+--------+------------+
14 rows in set (0.001 sec)
```

---

**Query 9:** Display the names of all employees working as clerks and drawing a salary more than 3,000.

```sql
SELECT ENAME, JOB, SAL FROM EMPLOYEE
WHERE JOB = 'CLERK' AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```

---

**Query 10:** Display the names of employees who are working as clerk, salesman or analyst and drawing a salary more than 3,000.

```sql
SELECT ENAME, JOB, SAL FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST')
AND SAL > 3000;
```

**Output:**
```
Empty set (0.001 sec)
```
