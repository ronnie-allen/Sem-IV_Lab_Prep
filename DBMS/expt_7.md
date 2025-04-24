# Ex-7: Aggregate and Built-in Functions

✅ **Objective**:  
Understand and use aggregate and built-in SQL functions to perform operations like summarizing data, manipulating strings, and working with numbers and dates.

---

## **Aggregate Functions**

### **1. SUM**  
**Concept**: Calculates the total sum of values in a numeric column.  
**Syntax**:  
```sql
SELECT SUM(column_name) FROM table_name;
```

---

### **2. COUNT**  
**Concept**: Counts the total number of rows in a table.  
**Syntax**:  
```sql
SELECT COUNT(*) FROM table_name;
```

---

### **3. MAX**  
**Concept**: Finds the largest value in a column.  
**Syntax**:  
```sql
SELECT MAX(column_name) FROM table_name;
```

---

### **4. MIN**  
**Concept**: Finds the smallest value in a column.  
**Syntax**:  
```sql
SELECT MIN(column_name) FROM table_name;
```

---

### **5. AVG**  
**Concept**: Calculates the average value of a numeric column.  
**Syntax**:  
```sql
SELECT AVG(column_name) FROM table_name;
```

---

## **Built-in Functions**

### **String Functions**

✅ **1. LENGTH**  
**Concept**: Returns the number of characters in a string.  
**Syntax**:  
```sql
SELECT LENGTH('example') FROM DUAL;
```

---

✅ **2. UPPER**  
**Concept**: Converts a string to uppercase.  
**Syntax**:  
```sql
SELECT UPPER('example') FROM DUAL;
```

---

✅ **3. SUBSTR**  
**Concept**: Extracts a substring from a string based on position and length.  
**Syntax**:  
```sql
SELECT SUBSTR('example', 2, 4) FROM DUAL;
```

---

### **Date Functions**

✅ **4. ADD_MONTHS**  
**Concept**: Adds a specified number of months to a date.  
**Syntax**:  
```sql
SELECT ADD_MONTHS(SYSDATE, 3) FROM DUAL;
```

---

### **Numeric Functions**

✅ **5. ROUND**  
**Concept**: Rounds a number to the specified number of decimal places.  
**Syntax**:  
```sql
SELECT ROUND(15.6789, 2) FROM DUAL;
```

---

✅ **6. TRUNC**  
**Concept**: Truncates a number to the specified number of decimal places.  
**Syntax**:  
```sql
SELECT TRUNC(15.6789, 2) FROM DUAL;
```

---

## **Unique Solution Queries**

✅ **1. Insert Data into Tables**  
(a) Insert records into the `Deposit_URK23AI1112` table.  
**SQL**:  
```sql
INSERT INTO Deposit_URK23AI1112 (actno, name, city, amount, acc_date)
VALUES (106, 'Sandip', 'Andheri', 2000, TO_DATE('31-MAR-96', 'DD-MON-YY'));
```
(b) Insert records into the `Branch_URK23AI1112` table.  
**SQL**:  
```sql
INSERT INTO Branch_URK23AI1112 (branch_name, branch_city)
VALUES ('Dharampeth', 'Nagpur');
```
(c) Insert records into the `Customer_URK23AI1112` table.  
**SQL**:  
```sql
INSERT INTO Customer_URK23AI1112 (cust_name, cust_city)
VALUES ('Pramod', 'Nagpur');
```
(d) Insert records into the `Borrow_URK23AI1112` table.  
**SQL**:  
```sql
INSERT INTO Borrow_URK23AI1112 (loan_no, cust_name, branch_name, loan_amount)
VALUES (481, 'Kranti', 'Nehru Place', 3000);
```

---

✅ **2. Total Loan Amount Taken by Borrowers**  
**SQL**:  
```sql
SELECT SUM(loan_amount) AS total_loan_amount FROM Borrow_URK23AI1112;
```

---

✅ **3. Total Deposit Done by Depositors**  
**SQL**:  
```sql
SELECT SUM(amount) AS total_deposit FROM Deposit_URK23AI1112;
```

---

✅ **4. Total Loan from Andheri Branch**  
**SQL**:  
```sql
SELECT SUM(loan_amount) AS total_loan_Andheri
FROM Borrow_URK23AI1112
WHERE branch_name = 'Andheri';
```

---

✅ **5. Deposits After 01-Jan-1996**  
**SQL**:  
```sql
SELECT SUM(amount) AS total_deposit_after_1996
FROM Deposit_URK23AI1112
WHERE acc_date > TO_DATE('01-JAN-96', 'DD-MON-YY');
```

---

✅ **6. Total Deposit of Customers in Nagpur**  
**SQL**:  
```sql
SELECT SUM(d.amount) AS total_deposit_Nagpur
FROM Deposit_URK23AI1112 d
JOIN Customer_URK23AI1112 c ON d.name = c.cust_name
WHERE c.cust_city = 'Nagpur';
```

---

✅ **7. Maximum Deposit of Customers in Bombay**  
**SQL**:  
```sql
SELECT MAX(d.amount) AS max_deposit_Bombay
FROM Deposit_URK23AI1112 d
JOIN Customer_URK23AI1112 c ON d.name = c.cust_name
WHERE c.cust_city = 'Bombay';
```

---

✅ **8. Total Branch Cities**  
**SQL**:  
```sql
SELECT COUNT(DISTINCT branch_city) AS total_branch_cities
FROM Branch_URK23AI1112;
```

---

✅ **9. Total Customer Cities**  
**SQL**:  
```sql
SELECT COUNT(DISTINCT cust_city) AS total_customer_cities
FROM Customer_URK23AI1112;
```

---

✅ **10. Branch-Wise Deposits**  
**SQL**:  
```sql
SELECT b.branch_name, SUM(d.amount) AS branch_wise_deposit
FROM Deposit_URK23AI1112 d
JOIN Branch_URK23AI1112 b ON d.city = b.branch_city
GROUP BY b.branch_name;
```

---

✅ **11. Deposits After 01-Jan-1996, Branch-Wise**  
**SQL**:  
```sql
SELECT b.branch_name, SUM(d.amount) AS branch_wise_deposit_after_1996
FROM Deposit_URK23AI1112 d
JOIN Branch_URK23AI1112 b ON d.city = b.branch_city
WHERE d.acc_date > TO_DATE('01-JAN-96', 'DD-MON-YY')
GROUP BY b.branch_name;
```

---

✅ **12. Branches with Deposits > 4000**  
**SQL**:  
```sql
SELECT b.branch_name, SUM(d.amount) AS total_deposit
FROM Deposit_URK23AI1112 d
JOIN Branch_URK23AI1112 b ON d.city = b.branch_city
GROUP BY b.branch_name
HAVING SUM(d.amount) > 4000;
```

---

✅ **13. Length of String 'dbms'**  
**SQL**:  
```sql
SELECT LENGTH('dbms') AS string_length FROM DUAL;
```

---

✅ **14. Customer Names in Uppercase**  
**SQL**:  
```sql
SELECT UPPER(cust_name) AS customer_name_uppercase
FROM Customer_URK23AI1112;
```

---

✅ **15. Substring "nil" from "Sunil"**  
**SQL**:  
```sql
SELECT SUBSTR('Sunil', 2, 3) AS extracted_substring FROM DUAL;
```

---

✅ **16. Prefix actno with Two Zeros**  
**SQL**:  
```sql
SELECT LPAD(actno, LENGTH(actno) + 2, '00') AS prefixed_actno
FROM Deposit_URK23AI1112;
```

---

✅ **17. Sort Deposit Table by actno**  
**SQL**:  
```sql
SELECT * FROM Deposit_URK23AI1112 ORDER BY actno;
```

---

✅ **18. Add Three Months to Current Date**  
**SQL**:  
```sql
SELECT ADD_MONTHS(SYSDATE, 3) AS new_date FROM DUAL;
```

---

✅ **19. Round and Truncate 15.6789**  
**SQL**:  
```sql
SELECT ROUND(15.6789, 2) AS rounded_value, TRUNC(15.6789, 2) AS truncated_value FROM DUAL;
```

---

## **CheatSheet**

| **Function Type**        | **Purpose**                        | **Syntax**                                          |
|---------------------------|-------------------------------------|----------------------------------------------------|
| **SUM**                  | Calculate total of values          | `SELECT SUM(column_name) FROM table_name;`         |
| **COUNT**                | Count number of rows               | `SELECT COUNT(*) FROM table_name;`                |
| **MAX**                  | Find the largest value             | `SELECT MAX(column_name) FROM table_name;`         |
| **MIN**                  | Find the smallest value            | `SELECT MIN(column_name) FROM table_name;`         |
| **AVG**                  | Find average value                 | `SELECT AVG(column_name) FROM table_name;`         |
|
---
