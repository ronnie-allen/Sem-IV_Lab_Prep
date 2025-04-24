Here’s the markdown for **Ex-4: SQL JOIN Operations**, keeping it brief, clear, and concise:

---

# **Ex-4: SQL JOIN Operations**

✅ **Objective**:  
Demonstrate the working of SQL Join operations to combine data from multiple tables based on relationships.

---

## **Join Types**

### **1. INNER JOIN**
- Returns matching rows from both tables based on a condition.  
**Syntax**:  
```sql
SELECT column_names FROM table1
INNER JOIN table2 ON table1.common_column = table2.common_column;
```

---

### **2. LEFT JOIN (LEFT OUTER JOIN)**
- Returns all rows from the left table and matching rows from the right.  
**Syntax**:  
```sql
SELECT column_names FROM table1
LEFT JOIN table2 ON table1.common_column = table2.common_column;
```

---

### **3. RIGHT JOIN (RIGHT OUTER JOIN)**
- Returns all rows from the right table and matching rows from the left.  
**Syntax**:  
```sql
SELECT column_names FROM table1
RIGHT JOIN table2 ON table1.common_column = table2.common_column;
```

---

### **4. FULL OUTER JOIN**
- Returns rows when there’s a match in either table, filling unmatched rows with `NULL`.  
**Syntax**:  
```sql
SELECT column_names FROM table1
FULL OUTER JOIN table2 ON table1.common_column = table2.common_column;
```

---

### **5. NATURAL JOIN**
- Joins two tables automatically based on common column names and data types.  
**Syntax**:  
```sql
SELECT column_names FROM table1
NATURAL JOIN table2;
```

---

### **6. CROSS JOIN (CARTESIAN JOIN)**
- Combines all rows from both tables, resulting in a Cartesian product.  
**Syntax**:  
```sql
SELECT column_names FROM table1
CROSS JOIN table2;
```

---

## **Unique Solution Questions**

✅ **1. Employee name, city, and salary (INNER JOIN)**  
**SQL**:  
```sql
SELECT e.employee_name, e.city, s.salary 
FROM employees e INNER JOIN salaries s 
ON e.employee_id = s.employee_id;
```

---

✅ **2. Cartesian product of managers and employees (CROSS JOIN)**  
**SQL**:  
```sql
SELECT m.manager_name, e.employee_name 
FROM managers m CROSS JOIN employees e;
```

---

✅ **3. Employees with salary > 3000 (ON Clause)**  
**SQL**:  
```sql
SELECT e.employee_name, m.manager_name, s.salary 
FROM employees e 
JOIN managers m ON e.manager_id = m.manager_id 
JOIN salaries s ON e.employee_id = s.employee_id 
WHERE s.salary > 3000;
```

---

✅ **4. Employees living and working in the same city**  
**SQL**:  
```sql
SELECT e.employee_name 
FROM employees e 
JOIN departments d ON e.employee_id = d.employee_id 
WHERE e.city = d.work_city;
```

---

✅ **5. Employees in Chennai with salary between 1500 and 10000**  
**SQL**:  
```sql
SELECT e.employee_name 
FROM employees e 
JOIN salaries s ON e.employee_id = s.employee_id 
WHERE e.city = 'Chennai' AND s.salary BETWEEN 1500 AND 10000;
```

---

✅ **6. Employees not assigned a living city**  
**SQL**:  
```sql
SELECT e.employee_name, e.company_name, s.salary 
FROM employees e 
JOIN salaries s ON e.employee_id = s.employee_id 
WHERE e.city IS NULL;
```

---

## **CheatSheet**

| **Join Type**        | **Purpose**                                       | **Syntax**                                                                 |
|-----------------------|---------------------------------------------------|-----------------------------------------------------------------------------|
| **INNER JOIN**        | Matching rows from both tables                   | `SELECT ... INNER JOIN ... ON condition;`                                   |
| **LEFT JOIN**         | All rows from the left, matches from the right   | `SELECT ... LEFT JOIN ... ON condition;`                                    |
| **RIGHT JOIN**        | All rows from the right, matches from the left   | `SELECT ... RIGHT JOIN ... ON condition;`                                   |
| **FULL OUTER JOIN**   | All rows from both tables, unmatched as `NULL`   | `SELECT ... FULL OUTER JOIN ... ON condition;`                              |
| **NATURAL JOIN**      | Joins tables on common column names and data types| `SELECT ... NATURAL JOIN ...;`                                              |
| **CROSS JOIN**        | Cartesian product of both tables                 | `SELECT ... CROSS JOIN ...;`                                                |

---

✅ **Conclusion**:  
Successfully demonstrated SQL Join operations to retrieve data efficiently across related tables.

---

Let me know if you’d like me to refine this further! 😊
