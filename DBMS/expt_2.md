# **Ex-2: Creating and Managing Tables**

✅ **Objective**:  
To learn the use of **Transaction Control Language (TCL)** and **Data Control Language (DCL)** for managing transactional processing and access control in a database.

---

## **Syntax**

### **TCL Commands**
1. **COMMIT**  
   - Saves all changes made during the current transaction permanently.  
   - **Syntax**:
     ```sql
     COMMIT;
     ```

2. **ROLLBACK**  
   - Reverts all changes made during the current transaction.  
   - **Syntax**:
     ```sql
     ROLLBACK;
     ```

3. **SAVEPOINT**  
   - Saves the current point in a transaction, allowing partial rollbacks.  
   - **Syntax**:
     ```sql
     SAVEPOINT savepoint_name;
     ```

---

### **DCL Commands**
1. **GRANT**  
   - Grants access privileges to a user.  
   - **Syntax**:
     ```sql
     GRANT privilege_type ON table_name TO user_id;
     ```

2. **REVOKE**  
   - Removes previously granted privileges from a user.  
   - **Syntax**:
     ```sql
     REVOKE privilege_type ON table_name FROM user_id;
     ```

---

## **Unique Solution Questions**

✅ **1. Grant SELECT and UPDATE Privileges**
**Task**: Allow the user `URK23AI1149` to view and modify the data in the `employees_URK23AI1112` table.  
**SQL Code**:
```sql
GRANT SELECT, UPDATE ON employees_URK23AI1112 TO URK23AI1149;
```

**Output**:
```plaintext
Grant succeeded.
```

---

✅ **2. Revoke a Specific Privilege**  
**Task**: Revoke the privilege of updating data in the `employees_URK23AI1112` table from user `URK23AI1149`.  
**SQL Code**:
```sql
REVOKE UPDATE ON employees_URK23AI1112 FROM URK23AI1149;
```

**Output**:
```plaintext
Revoke succeeded.
```

---

✅ **3. Rollback to a Savepoint**  
**Task**: Rollback changes to the state saved at a specific savepoint `before_update`.  
**SQL Code**:
```sql
ROLLBACK TO SAVEPOINT before_update;
```

**Output**:
```plaintext
Rollback complete.
```

---

✅ **4. Commit a Transaction**  
**Task**: Save the changes permanently to the database.  
**SQL Code**:
```sql
COMMIT;
```

**Output**:
```plaintext
Commit complete.
```

---

✅ **5. Create a Savepoint**  
**Task**: Create a savepoint named `before_update` to allow rolling back to this point later.  
**SQL Code**:
```sql
SAVEPOINT before_update;
```

**Output**:
```plaintext
Savepoint created.
```

---

✅ **6. View Data After Savepoint and Rollback**  
**Task**: Check if changes made after a savepoint are undone after a rollback.  
**SQL Code**:
```sql
SELECT * FROM employees_URK23AI1112;
```

**Output**:
```plaintext
ID      FIRST_NAME    LAST_NAME    DATEOFBIR    PHONE_NUMBER
1128    JERICKSON     JACOBRAJ     18-JAN-06    9456785679
1149    ABUnesh       RP           01-FEB-06    9456785679
1118    JOEL                       10-JUL-05    9456785679
```

---

## **CheatSheet**

### **TCL (Transaction Control Language)**

| **Command**       | **Purpose**                                         | **Syntax**                       |
|--------------------|-----------------------------------------------------|-----------------------------------|
| **COMMIT**         | Save all changes permanently                        | `COMMIT;`                        |
| **ROLLBACK**       | Undo changes made in the current transaction        | `ROLLBACK;`                      |
| **SAVEPOINT**      | Save the current transaction state for rollback     | `SAVEPOINT savepoint_name;`      |
| **ROLLBACK TO**    | Rollback to a specific savepoint                    | `ROLLBACK TO SAVEPOINT savepoint_name;` |

---

### **DCL (Data Control Language)**

| **Command**        | **Purpose**                                         | **Syntax**                                   |
|---------------------|-----------------------------------------------------|---------------------------------------------|
| **GRANT**          | Assign specific privileges to a user                | `GRANT privilege_type ON table_name TO user_id;` |
| **REVOKE**         | Remove specific privileges from a user              | `REVOKE privilege_type ON table_name FROM user_id;` |

---

### **Key Points**
1. **Transactions**: Use `COMMIT` and `ROLLBACK` to manage transactional states.
2. **Access Control**: Control who can view or modify data using `GRANT` and `REVOKE`.
3. **Savepoints**: Use `SAVEPOINT` to create points in a transaction for partial rollbacks.

✅ **Conclusion**: Successfully learned and implemented TCL and DCL commands to manage transactions and control database access.

---
