
# **Ex-3: Set Operations in SQL**

✅ **Objective**:  
Demonstrate the usage of **set operations** (UNION, UNION ALL, INTERSECT, EXCEPT) in SQL for combining and filtering query results.

---

### **Concepts**

1. **UNION**  
   Combines results of two or more SELECT statements and removes duplicate rows.  
   **Example**:  
   ```sql
   SELECT city FROM Company
   UNION
   SELECT city FROM Employee;
   ```

2. **UNION ALL**  
   Combines results of SELECT statements but includes duplicates.  
   **Example**:  
   ```sql
   SELECT city FROM Company
   UNION ALL
   SELECT city FROM Employee;
   ```

3. **INTERSECT**  
   Returns rows that are common to both SELECT statements.  
   **Example**:  
   ```sql
   SELECT city FROM Company
   INTERSECT
   SELECT city FROM Employee;
   ```

4. **EXCEPT (or MINUS)**  
   Returns rows from the first SELECT statement that are not in the second.  
   **Example**:  
   ```sql
   SELECT city FROM Company
   EXCEPT
   SELECT city FROM Employee;
   ```

---

### **Unique Solution Questions**

✅ **1. Display the cities of companies 'ACC' and 'TATA'**  
**SQL**:
```sql
SELECT city FROM Company WHERE company_name IN ('ACC', 'TATA');
```
**Output**:
```plaintext
CITY
------
Nagpur
Bombay
```

✅ **2. Find the cities where 'ACC' is located but not in 'TATA'**  
**SQL**:
```sql
SELECT city FROM Company WHERE company_name = 'ACC'
MINUS
SELECT city FROM Company WHERE company_name = 'TATA';
```
**Output**:
```plaintext
CITY
------
Nagpur
```

✅ **3. Display the names of employees living in Nagpur and working for 'ACC'**  
**SQL**:
```sql
SELECT e.emp_name
FROM Employee e
JOIN Emp_Company ec ON e.emp_name = ec.emp_name
WHERE e.city = 'Nagpur' AND ec.company_name = 'ACC';
```
**Output**:
```plaintext
EMP_NAME
---------
Amit
Suresh
```

✅ **4. List employees living in Bombay with a salary >1500**  
**SQL**:
```sql
SELECT e.emp_name
FROM Employee e
JOIN Emp_Company ec ON e.emp_name = ec.emp_name
WHERE e.city = 'Bombay' AND ec.salary > 1500;
```
**Output**:
```plaintext
EMP_NAME
---------
Priya
Raj
```

✅ **5. Find employees living in Chennai and working with 'CMC'**  
**SQL**:
```sql
SELECT e.emp_name
FROM Employee e
JOIN Emp_Company ec ON e.emp_name = ec.emp_name
WHERE e.city = 'Chennai' AND ec.company_name = 'CMC';
```
**Output**:
```plaintext
EMP_NAME
---------
Neha
```

✅ **6. Employees living in Nagpur, working in 'ACC', and in shift 'A'**  
**SQL**:
```sql
SELECT e.emp_name
FROM Employee e
JOIN Emp_Company ec ON e.emp_name = ec.emp_name
JOIN Emp_Shift es ON e.emp_name = es.emp_name
WHERE e.city = 'Nagpur' AND ec.company_name = 'ACC' AND es.shift = 'A';
```
**Output**:
```plaintext
EMP_NAME
---------
Amit
```

✅ **7. Employees living in Nagpur or Bombay**  
**SQL**:
```sql
SELECT * FROM Employee WHERE city IN ('Nagpur', 'Bombay');
```
**Output**:
```plaintext
EMP_NAME    CITY
---------   --------
Amit        Nagpur
Priya       Bombay
Suresh      Nagpur
Raj         Bombay
```

---

### **CheatSheet**

| **Set Operation**  | **Purpose**                                         | **Syntax**                                                      |
|---------------------|-----------------------------------------------------|-----------------------------------------------------------------|
| **UNION**          | Combine unique rows from multiple SELECT statements | `SELECT ... UNION SELECT ...;`                                  |
| **UNION ALL**      | Combine all rows (including duplicates)             | `SELECT ... UNION ALL SELECT ...;`                              |
| **INTERSECT**      | Return only common rows                             | `SELECT ... INTERSECT SELECT ...;`                              |
| **EXCEPT (MINUS)** | Return rows in the first query but not in the second| `SELECT ... EXCEPT SELECT ...;`                                 |

---

✅ **Conclusion**:  
Successfully demonstrated SQL **set operations** (UNION, INTERSECT, EXCEPT) and their application to combine and filter query results effectively.

---

Let me know if this format works or if you'd like further tweaks! 😊
