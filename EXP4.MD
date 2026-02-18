<div align="center">
  <h1>Experiment 04</h1>
</div>

**Perform Following Queries using Employee Table (Retrieving Data)**

---

**Query 1:** Display the list of employees who have joined the company before 30th June 80 or after 31st Dec 81.

```sql
SELECT * FROM EMPLOYEE
WHERE HIREDATE < '1980-06-30'
OR HIREDATE > '1981-12-31';
```

**Output:**
```
+-------+--------+---------+------+------------+---------+------+--------+
| EMPNO | ENAME  | JOB     | MGR  | HIREDATE   | SAL     | COMM | DEPTNO |
+-------+--------+---------+------+------------+---------+------+--------+
|  7788 | SCOTT  | ANALYST | 7566 | 1987-04-19 | 3000.00 | NULL |     20 |
|  7876 | ADAMS  | CLERK   | 7788 | 1987-05-23 | 1100.00 | NULL |     20 |
|  7934 | MILLER | CLERK   | 7782 | 1982-01-23 | 1300.00 | NULL |     10 |
+-------+--------+---------+------+------------+---------+------+--------+
3 rows in set (0.001 sec)
```

---

**Query 2:** Display the names of employees whose names have second alphabet A in their names.

```sql
SELECT ENAME FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
```

---

**Query 3:** Display the names of employees whose name is exactly five characters in length.

```sql
SELECT ENAME FROM EMPLOYEE
WHERE LENGTH(ENAME) = 5;
```

**Output:**
```
+-------+
| ENAME |
+-------+
| SMITH |
| ALLEN |
| JONES |
| BLAKE |
| CLARK |
| SCOTT |
| ADAMS |
| JAMES |
+-------+
8 rows in set (0.001 sec)
```

---

**Query 4:** Display the names of employees whose names have second alphabet A in their names.

```sql
SELECT ENAME FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

**Output:**
```
+--------+
| ENAME  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.001 sec)
```

---

**Query 5:** Display the names of employees who are not working as salesman or clerk or analyst.

```sql
SELECT ENAME, JOB FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
```

**Output:**
```
+-------+-----------+
| ENAME | JOB       |
+-------+-----------+
| JONES | MANAGER   |
| BLAKE | MANAGER   |
| CLARK | MANAGER   |
| KING  | PRESIDENT |
+-------+-----------+
4 rows in set (0.001 sec)
```

---

**Query 6:** Display the name of the employee along with their annual salary (sal*12). The name of the employee earning highest salary should appear first.

```sql
SELECT ENAME, SAL * 12 AS ANNUAL_SAL
FROM EMPLOYEE
ORDER BY ANNUAL_SAL DESC;
```

**Output:**
```
+--------+------------+
| ENAME  | ANNUAL_SAL |
+--------+------------+
| KING   |   60000.00 |
| SCOTT  |   36000.00 |
| FORD   |   36000.00 |
| JONES  |   35700.00 |
| BLAKE  |   34200.00 |
| CLARK  |   29400.00 |
| ALLEN  |   19200.00 |
| TURNER |   18000.00 |
| MILLER |   15600.00 |
| WARD   |   15000.00 |
| MARTIN |   15000.00 |
| ADAMS  |   13200.00 |
| JAMES  |   11400.00 |
| SMITH  |    9600.00 |
+--------+------------+
14 rows in set (0.001 sec)
```

---

**Query 7:** Display name, sal, hra, pf, da, totalsal for each employee. HRA 15% of sal, DA 10% of sal, PF 5% of sal. Total salary = (sal + hra + da) - pf. Output in the order of total sal.

```sql
SELECT ENAME, SAL,
       SAL * 0.15 AS HRA,
       SAL * 0.10 AS DA,
       SAL * 0.05 AS PF,
       (SAL + SAL * 0.15 + SAL * 0.10) - SAL * 0.05 AS TOTALSAL
FROM EMPLOYEE
ORDER BY TOTALSAL DESC;
```

**Output:**
```
+--------+---------+--------+--------+--------+----------+
| ENAME  | SAL     | HRA    | DA     | PF     | TOTALSAL |
+--------+---------+--------+--------+--------+----------+
| KING   | 5000.00 | 750.00 | 500.00 | 250.00 |  6000.00 |
| SCOTT  | 3000.00 | 450.00 | 300.00 | 150.00 |  3600.00 |
| FORD   | 3000.00 | 450.00 | 300.00 | 150.00 |  3600.00 |
| JONES  | 2975.00 | 446.25 | 297.50 | 148.75 |  3570.00 |
| BLAKE  | 2850.00 | 427.50 | 285.00 | 142.50 |  3420.00 |
| CLARK  | 2450.00 | 367.50 | 245.00 | 122.50 |  2940.00 |
| ALLEN  | 1600.00 | 240.00 | 160.00 |  80.00 |  1920.00 |
| TURNER | 1500.00 | 225.00 | 150.00 |  75.00 |  1800.00 |
| MILLER | 1300.00 | 195.00 | 130.00 |  65.00 |  1560.00 |
| WARD   | 1250.00 | 187.50 | 125.00 |  62.50 |  1500.00 |
| MARTIN | 1250.00 | 187.50 | 125.00 |  62.50 |  1500.00 |
| ADAMS  | 1100.00 | 165.00 | 110.00 |  55.00 |  1320.00 |
| JAMES  |  950.00 | 142.50 |  95.00 |  47.50 |  1140.00 |
| SMITH  |  800.00 | 120.00 |  80.00 |  40.00 |   960.00 |
+--------+---------+--------+--------+--------+----------+
14 rows in set (0.001 sec)
```

---

**Query 8:** Update the salary of each employee by 10% increment who are not eligible for commission.

```sql
UPDATE EMPLOYEE
SET SAL = SAL * 1.10
WHERE COMM IS NULL;
```

**Output:**
```
Query OK, 10 rows affected (0.005 sec)
Rows matched: 10  Changed: 10  Warnings: 0
```

```sql
SELECT EMPNO, ENAME, SAL, COMM FROM EMPLOYEE;
```

**Output:**
```
+-------+--------+---------+---------+
| EMPNO | ENAME  | SAL     | COMM    |
+-------+--------+---------+---------+
|  7369 | SMITH  |  880.00 |    NULL |
|  7499 | ALLEN  | 1600.00 |  300.00 |
|  7521 | WARD   | 1250.00 |  300.00 |
|  7566 | JONES  | 3272.50 |    NULL |
|  7654 | MARTIN | 1250.00 | 1400.00 |
|  7698 | BLAKE  | 3135.00 |    NULL |
|  7782 | CLARK  | 2695.00 |    NULL |
|  7788 | SCOTT  | 3300.00 |    NULL |
|  7839 | KING   | 5500.00 |    NULL |
|  7844 | TURNER | 1500.00 |    0.00 |
|  7876 | ADAMS  | 1210.00 |    NULL |
|  7900 | JAMES  | 1045.00 |    NULL |
|  7902 | FORD   | 3300.00 |    NULL |
|  7934 | MILLER | 1430.00 |    NULL |
+-------+--------+---------+---------+
14 rows in set (0.001 sec)
```

---

**Query 9:** Display those employees whose salary is more than 3000 after giving 20% increment.

```sql
SELECT ENAME, SAL, SAL * 1.20 AS SAL_AFTER_INC
FROM EMPLOYEE
WHERE SAL * 1.20 > 3000;
```

**Output:**
```
+-------+---------+---------------+
| ENAME | SAL     | SAL_AFTER_INC |
+-------+---------+---------------+
| JONES | 3272.50 |       3927.00 |
| BLAKE | 3135.00 |       3762.00 |
| CLARK | 2695.00 |       3234.00 |
| SCOTT | 3300.00 |       3960.00 |
| KING  | 5500.00 |       6600.00 |
| FORD  | 3300.00 |       3960.00 |
+-------+---------+---------------+
6 rows in set (0.001 sec)
```

---

**Query 10:** Display those employees whose salary contains at least 3 digits.

```sql
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL >= 100;
```

**Output:**
```
+--------+---------+
| ENAME  | SAL     |
+--------+---------+
| SMITH  |  880.00 |
| ALLEN  | 1600.00 |
| WARD   | 1250.00 |
| JONES  | 3272.50 |
| MARTIN | 1250.00 |
| BLAKE  | 3135.00 |
| CLARK  | 2695.00 |
| SCOTT  | 3300.00 |
| KING   | 5500.00 |
| TURNER | 1500.00 |
| ADAMS  | 1210.00 |
| JAMES  | 1045.00 |
| FORD   | 3300.00 |
| MILLER | 1430.00 |
+--------+---------+
14 rows in set (0.001 sec)
```
