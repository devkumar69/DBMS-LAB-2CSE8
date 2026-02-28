<div align="center">
  <h1>Experiment 07</h1>
</div>

**Perform Following Queries using Employee Table (Date Functions, Aggregate Functions & Group By)**

---

**Query 1:** Compute the number of days remaining in this year.

```sql
SELECT DATEDIFF(
  CONCAT(YEAR(CURDATE()), '-12-31'), CURDATE()
) AS DAYS_REMAINING;
```

**Output:**
```
+----------------+
| DAYS_REMAINING |
+----------------+
|            306 |
+----------------+
1 row in set (0.001 sec)
```

---

**Query 2:** Find the highest and lowest salaries and the difference between them.

```sql
SELECT
  MAX(SAL) AS HIGHEST_SALARY,
  MIN(SAL) AS LOWEST_SALARY,
  MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

**Output:**
```
+----------------+---------------+------------+
| HIGHEST_SALARY | LOWEST_SALARY | DIFFERENCE |
+----------------+---------------+------------+
|        5000.00 |        800.00 |    4200.00 |
+----------------+---------------+------------+
1 row in set (0.001 sec)
```

---

**Query 3:** List employees whose commission is greater than 25% of their salaries.

```sql
SELECT EMPNO, ENAME, SAL, COMM
FROM EMPLOYEE
WHERE COMM > SAL * 0.25;
```

**Output:**
```
+-------+--------+---------+---------+
| EMPNO | ENAME  | SAL     | COMM    |
+-------+--------+---------+---------+
|  7654 | MARTIN | 1250.00 | 1400.00 |
+-------+--------+---------+---------+
1 row in set (0.001 sec)
```

---

**Query 4:** Make a query that displays salary in dollar format.

```sql
SELECT EMPNO, ENAME, CONCAT('$', FORMAT(SAL, 2)) AS SALARY_IN_DOLLARS
FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+-------------------+
| EMPNO | ENAME  | SALARY_IN_DOLLARS |
+-------+--------+-------------------+
|  7369 | SMITH  | $800.00           |
|  7499 | ALLEN  | $1,600.00         |
|  7521 | WARD   | $1,250.00         |
|  7566 | JONES  | $2,975.00         |
|  7654 | MARTIN | $1,250.00         |
|  7698 | BLAKE  | $2,850.00         |
|  7782 | CLARK  | $2,450.00         |
|  7788 | SCOTT  | $3,000.00         |
|  7839 | KING   | $5,000.00         |
|  7844 | TURNER | $1,500.00         |
|  7876 | ADAMS  | $1,100.00         |
|  7900 | JAMES  | $950.00           |
|  7902 | FORD   | $3,000.00         |
|  7934 | MILLER | $1,300.00         |
+-------+--------+-------------------+
14 rows in set (0.001 sec)
```

---

**Query 5:** Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.

```sql
SELECT JOB,
  SUM(CASE WHEN DEPTNO = 10 THEN SAL ELSE 0 END) AS DEPT_10,
  SUM(CASE WHEN DEPTNO = 20 THEN SAL ELSE 0 END) AS DEPT_20,
  SUM(CASE WHEN DEPTNO = 30 THEN SAL ELSE 0 END) AS DEPT_30,
  SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
ORDER BY JOB;
```

**Output:**
```
+-----------+---------+---------+---------+--------------+
| JOB       | DEPT_10 | DEPT_20 | DEPT_30 | TOTAL_SALARY |
+-----------+---------+---------+---------+--------------+
| ANALYST   |    0.00 | 6000.00 |    0.00 |      6000.00 |
| CLERK     | 1300.00 | 1900.00 |  950.00 |      4150.00 |
| MANAGER   | 2450.00 | 2975.00 | 2850.00 |      8275.00 |
| PRESIDENT | 5000.00 |    0.00 |    0.00 |      5000.00 |
| SALESMAN  |    0.00 |    0.00 | 5600.00 |      5600.00 |
+-----------+---------+---------+---------+--------------+
5 rows in set (0.001 sec)
```

---

**Query 6:** Query that will display the total number of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column headings.

```sql
SELECT
  COUNT(*) AS TOTAL_EMPLOYEES,
  SUM(CASE WHEN YEAR(HIREDATE) = 1980 THEN 1 ELSE 0 END) AS HIRED_IN_1980,
  SUM(CASE WHEN YEAR(HIREDATE) = 1981 THEN 1 ELSE 0 END) AS HIRED_IN_1981,
  SUM(CASE WHEN YEAR(HIREDATE) = 1982 THEN 1 ELSE 0 END) AS HIRED_IN_1982,
  SUM(CASE WHEN YEAR(HIREDATE) = 1983 THEN 1 ELSE 0 END) AS HIRED_IN_1983
FROM EMPLOYEE;
```

**Output:**
```
+-----------------+---------------+---------------+---------------+---------------+
| TOTAL_EMPLOYEES | HIRED_IN_1980 | HIRED_IN_1981 | HIRED_IN_1982 | HIRED_IN_1983 |
+-----------------+---------------+---------------+---------------+---------------+
|              14 |             1 |            10 |             1 |             0 |
+-----------------+---------------+---------------+---------------+---------------+
1 row in set (0.001 sec)
```

---

**Query 7:** Query to get the last Sunday of any month.

```sql
SELECT
  LAST_DAY(CURDATE()) AS LAST_DAY_OF_MONTH,
  DATE_SUB(
    LAST_DAY(CURDATE()),
    INTERVAL (DAYOFWEEK(LAST_DAY(CURDATE())) - 1) DAY
  ) AS LAST_SUNDAY;
```

**Output:**
```
+-------------------+-------------+
| LAST_DAY_OF_MONTH | LAST_SUNDAY |
+-------------------+-------------+
| 2026-02-28        | 2026-02-22  |
+-------------------+-------------+
1 row in set (0.001 sec)
```

---

**Query 8:** Display department numbers and total number of employees working in each department.

```sql
SELECT DEPTNO, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+-----------------+
| DEPTNO | TOTAL_EMPLOYEES |
+--------+-----------------+
|     10 |               3 |
|     20 |               5 |
|     30 |               6 |
+--------+-----------------+
3 rows in set (0.001 sec)
```

---

**Query 9:** Display the various jobs and total number of employees within each job group.

```sql
SELECT JOB, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB
ORDER BY JOB;
```

**Output:**
```
+-----------+-----------------+
| JOB       | TOTAL_EMPLOYEES |
+-----------+-----------------+
| ANALYST   |               2 |
| CLERK     |               4 |
| MANAGER   |               3 |
| PRESIDENT |               1 |
| SALESMAN  |               4 |
+-----------+-----------------+
5 rows in set (0.001 sec)
```

---

**Query 10:** Display the department numbers and total salary for each department.

```sql
SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO
ORDER BY DEPTNO;
```

**Output:**
```
+--------+--------------+
| DEPTNO | TOTAL_SALARY |
+--------+--------------+
|     10 |      8750.00 |
|     20 |     10875.00 |
|     30 |      9400.00 |
+--------+--------------+
3 rows in set (0.001 sec)
```
