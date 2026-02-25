<div align="center">
  <h1>Experiment 06</h1>
</div>

**Perform Following Queries using Employee Table (Date Functions & Conversion Functions)**

---

**Query 1:** Display empno, ename, deptno from employee table. Instead of displaying department numbers, display the related department name (Use DECODE function equivalent — CASE in MySQL).

```sql
SELECT EMPNO, ENAME,
  CASE DEPTNO
    WHEN 10 THEN 'ACCOUNTING'
    WHEN 20 THEN 'RESEARCH'
    WHEN 30 THEN 'SALES'
    WHEN 40 THEN 'OPERATIONS'
    ELSE 'UNKNOWN'
  END AS DNAME
FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+------------+
| EMPNO | ENAME  | DNAME      |
+-------+--------+------------+
|  7369 | SMITH  | RESEARCH   |
|  7499 | ALLEN  | SALES      |
|  7521 | WARD   | SALES      |
|  7566 | JONES  | RESEARCH   |
|  7654 | MARTIN | SALES      |
|  7698 | BLAKE  | SALES      |
|  7782 | CLARK  | ACCOUNTING |
|  7788 | SCOTT  | RESEARCH   |
|  7839 | KING   | ACCOUNTING |
|  7844 | TURNER | SALES      |
|  7876 | ADAMS  | RESEARCH   |
|  7900 | JAMES  | SALES      |
|  7902 | FORD   | RESEARCH   |
|  7934 | MILLER | ACCOUNTING |
+-------+--------+------------+
14 rows in set (0.001 sec)
```

---

**Query 2:** Display your age in days.

```sql
SELECT DATEDIFF(CURDATE(), '2005-06-15') AS AGE_IN_DAYS;
```

**Output:**
```
+-------------+
| AGE_IN_DAYS |
+-------------+
|        7560 |
+-------------+
1 row in set (0.001 sec)
```

---

**Query 3:** Display your age in months.

```sql
SELECT TIMESTAMPDIFF(MONTH, '2005-06-15', CURDATE()) AS AGE_IN_MONTHS;
```

**Output:**
```
+---------------+
| AGE_IN_MONTHS |
+---------------+
|           248 |
+---------------+
1 row in set (0.001 sec)
```

---

**Query 4:** Display the current date as "15th August Friday Nineteen Ninety-Seven" format.

```sql
SELECT DATE_FORMAT(CURDATE(), '%D %M %W %Y') AS FORMATTED_DATE;
```

**Output:**
```
+----------------------------------+
| FORMATTED_DATE                   |
+----------------------------------+
| 25th February Wednesday 2026     |
+----------------------------------+
1 row in set (0.001 sec)
```

---

**Query 5 & 6:** Display the following output for each row from employee table — "Scott has joined the company on Wednesday 13th August Nineteen Ninety" format.

```sql
SELECT CONCAT(
  CONCAT(UPPER(SUBSTRING(ENAME, 1, 1)), LOWER(SUBSTRING(ENAME, 2))),
  ' has joined the company on ',
  DATE_FORMAT(HIREDATE, '%W %D %M %Y')
) AS EMPLOYEE_INFO
FROM EMPLOYEE;
```

**Output:**
```
+--------------------------------------------------------------+
| EMPLOYEE_INFO                                                |
+--------------------------------------------------------------+
| Smith has joined the company on Wednesday 17th December 1980 |
| Allen has joined the company on Friday 20th February 1981    |
| Ward has joined the company on Sunday 22nd February 1981     |
| Jones has joined the company on Thursday 2nd April 1981      |
| Martin has joined the company on Monday 28th September 1981  |
| Blake has joined the company on Friday 1st May 1981          |
| Clark has joined the company on Tuesday 9th June 1981        |
| Scott has joined the company on Sunday 19th April 1987       |
| King has joined the company on Tuesday 17th November 1981    |
| Turner has joined the company on Tuesday 8th September 1981  |
| Adams has joined the company on Saturday 23rd May 1987       |
| James has joined the company on Thursday 3rd December 1981   |
| Ford has joined the company on Thursday 3rd December 1981    |
| Miller has joined the company on Saturday 23rd January 1982  |
+--------------------------------------------------------------+
14 rows in set (0.001 sec)
```

---

**Query 7:** Find the date for nearest Saturday after current date.

```sql
SELECT DATE_ADD(CURDATE(), INTERVAL (7 - DAYOFWEEK(CURDATE())) DAY) AS NEXT_SATURDAY;
```

**Output:**
```
+---------------+
| NEXT_SATURDAY |
+---------------+
| 2026-02-28    |
+---------------+
1 row in set (0.001 sec)
```

---

**Query 8:** Display current time.

```sql
SELECT CURTIME() AS TIME_NOW;
```

**Output:**
```
+----------+
| TIME_NOW |
+----------+
| 10:30:45 |
+----------+
1 row in set (0.001 sec)
```

---

**Query 9:** Display the date three months before the current date.

```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 3 MONTH) AS DATE_BEFORE_3_MONTHS;
```

**Output:**
```
+----------------------+
| DATE_BEFORE_3_MONTHS |
+----------------------+
| 2025-11-25           |
+----------------------+
1 row in set (0.001 sec)
```

---

**Query 10:** Display those employees who joined in the company in the month of Dec.

```sql
SELECT * FROM EMPLOYEE
WHERE MONTH(HIREDATE) = 12;
```

**Output:**
```
+-------+-------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+-------+---------+------+------------+---------+------+--------+
|  7369 | SMITH | CLERK   | 7902 | 1980-12-17 |  800.00 | NULL |     20 |
|  7900 | JAMES | CLERK   | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD  | ANALYST | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+-------+---------+------+------------+---------+------+--------+
3 rows in set (0.001 sec)
```

---

**Query 11:** Display those employees whose first 2 characters from hire date and last 2 characters of salary.

```sql
SELECT ENAME,
  LEFT(DATE_FORMAT(HIREDATE, '%d'), 2) AS FIRST_2_HIREDATE,
  RIGHT(CAST(SAL AS SIGNED), 2) AS LAST_2_SAL
FROM EMPLOYEE;
```

**Output:**
```
+--------+------------------+------------+
| ENAME  | FIRST_2_HIREDATE | LAST_2_SAL |
+--------+------------------+------------+
| SMITH  | 17               | 00         |
| ALLEN  | 20               | 00         |
| WARD   | 22               | 50         |
| JONES  | 02               | 75         |
| MARTIN | 28               | 50         |
| BLAKE  | 01               | 50         |
| CLARK  | 09               | 50         |
| SCOTT  | 19               | 00         |
| KING   | 17               | 00         |
| TURNER | 08               | 00         |
| ADAMS  | 23               | 00         |
| JAMES  | 03               | 50         |
| FORD   | 03               | 00         |
| MILLER | 23               | 00         |
+--------+------------------+------------+
14 rows in set (0.001 sec)
```

---

**Query 12:** Display those employees whose 10% of salary is equal to the year of joining.

```sql
SELECT * FROM EMPLOYEE
WHERE SAL * 0.10 = YEAR(HIREDATE) % 100;
```

**Output:**
```
+-------+-------+-------+------+------------+--------+------+--------+
| EMPNO | ENAME | JOB   | MGR  | HIREDATE   | SAL    | COMM | DEPTNO |
+-------+-------+-------+------+------------+--------+------+--------+
|  7369 | SMITH | CLERK | 7902 | 1980-12-17 | 800.00 | NULL |     20 |
+-------+-------+-------+------+------------+--------+------+--------+
1 row in set (0.001 sec)
```

---

**Query 13:** Display those employees who joined the company before 15 of the month.

```sql
SELECT * FROM EMPLOYEE
WHERE DAY(HIREDATE) < 15;
```

**Output:**
```
+-------+--------+----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+----------+------+------------+---------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2450.00 | NULL |     10 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 | 0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+--------+----------+------+------------+---------+------+--------+
6 rows in set (0.001 sec)
```

---

**Query 14:** Display those employees who has joined before 15th of the month.

```sql
SELECT * FROM EMPLOYEE
WHERE EXTRACT(DAY FROM HIREDATE) < 15;
```

**Output:**
```
+-------+--------+----------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB      | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+----------+------+------------+---------+------+--------+
|  7566 | JONES  | MANAGER  | 7839 | 1981-04-02 | 2975.00 | NULL |     20 |
|  7698 | BLAKE  | MANAGER  | 7839 | 1981-05-01 | 2850.00 | NULL |     30 |
|  7782 | CLARK  | MANAGER  | 7839 | 1981-06-09 | 2450.00 | NULL |     10 |
|  7844 | TURNER | SALESMAN | 7698 | 1981-09-08 | 1500.00 | 0.00 |     30 |
|  7900 | JAMES  | CLERK    | 7698 | 1981-12-03 |  950.00 | NULL |     30 |
|  7902 | FORD   | ANALYST  | 7566 | 1981-12-03 | 3000.00 | NULL |     20 |
+-------+--------+----------+------+------------+---------+------+--------+
6 rows in set (0.001 sec)
```

---

**Query 15:** Display those employees whose joining DATE is available in deptno.

```sql
SELECT * FROM EMPLOYEE
WHERE DAY(HIREDATE) IN (SELECT DISTINCT DEPTNO FROM EMPLOYEE);
```

**Output:**
```
+-------+-------+----------+------+------------+---------+--------+--------+
| EMPNO | ENAME | JOB      | MGR  | HIREDATE   | SAL     | COMM   | DEPTNO |
+-------+-------+----------+------+------------+---------+--------+--------+
|  7499 | ALLEN | SALESMAN | 7698 | 1981-02-20 | 1600.00 | 300.00 |     30 |
+-------+-------+----------+------+------------+---------+--------+--------+
1 row in set (0.001 sec)
```
