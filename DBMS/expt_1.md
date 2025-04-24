# **Ex-1: Creating and Managing Tables**

✅ **1. Create a table for a Student**  
**Concept**:  
Creating a table defines the structure for storing data in a relational database. It includes attributes (columns) and constraints like `PRIMARY KEY`, `NOT NULL`, and `UNIQUE`.  

**SQL Syntax**:
```sql
CREATE TABLE Student (
    student_id NUMBER(5) PRIMARY KEY,
    student_name CHAR(20) UNIQUE,
    dept CHAR(10) NOT NULL,
    age NUMBER(2)
);
```

**Output**:
```plaintext
Table created.
```

---

✅ **2. Add attributes to the Student table**  
**Concept**:  
Use the `ALTER TABLE` command to modify an existing table. You can add new attributes (columns) with specified data types.

**SQL Syntax (Add Grade)**:
```sql
ALTER TABLE Student ADD grade VARCHAR2(5);
```
**Output**:
```plaintext
Table altered.
```

**SQL Syntax (Add City)**:
```sql
ALTER TABLE Student ADD city CHAR(20);
```
**Output**:
```plaintext
Table altered.
```

---

✅ **3. Modify the table structure**  
**Task**: Rename the `city` column to `address`.  
**Concept**:  
Renaming a column in an existing table uses the `ALTER TABLE` command.  

**SQL Syntax**:
```sql
ALTER TABLE Student RENAME COLUMN city TO address;
```

**Output**:
```plaintext
Table altered.
```

---

✅ **4. Drop the Student table**  
**Concept**:  
`DROP TABLE` removes the table and all its data permanently.  

**SQL Syntax**:
```sql
DROP TABLE Student;
```

**Output**:
```plaintext
Table dropped.
```

---

✅ **5. Truncate the Student table**  
**Concept**:  
`TRUNCATE TABLE` removes all rows from a table while keeping its structure intact.  

**SQL Syntax**:
```sql
TRUNCATE TABLE Student;
```

**Output**:
```plaintext
Table truncated.
```

---

### **CheatSheet**
🧾 **DDL (Data Definition Language) Cheatsheet**  
Task | Purpose | Syntax  
--- | --- | ---  
Create Table | Define a new table | `CREATE TABLE table_name (...);`  
Add Column | Add a new attribute to a table | `ALTER TABLE table_name ADD column_name datatype;`  
Rename Column | Change the name of an existing column | `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;`  
Drop Table | Remove a table entirely | `DROP TABLE table_name;`  
Truncate Table | Remove all rows but keep structure | `TRUNCATE TABLE table_name;`  

---


### **CheatSheet: DDL (Data Definition Language)**

| **Command**        | **Purpose**                                      | **Syntax**                                                                 |
|---------------------|--------------------------------------------------|-----------------------------------------------------------------------------|
| **Create Table**    | Define a new table                               | `CREATE TABLE table_name (column1 datatype constraint, column2 datatype constraint, ...);` |
| **Add Column**      | Add a new attribute (column) to an existing table| `ALTER TABLE table_name ADD column_name datatype;`                         |
| **Drop Column**     | Remove a column from a table                     | `ALTER TABLE table_name DROP COLUMN column_name;`                          |
| **Rename Column**   | Change the name of an existing column            | `ALTER TABLE table_name RENAME COLUMN old_name TO new_name;`               |
| **Drop Table**      | Permanently delete the table and all its data    | `DROP TABLE table_name;`                                                   |
| **Truncate Table**  | Remove all rows but keep the table structure     | `TRUNCATE TABLE table_name;`                                               |

---

### **Explanation of Key Commands**

1. **Create Table**:  
   - Use this to define a new table with columns and constraints (e.g., `PRIMARY KEY`, `NOT NULL`).  
   - **Example**:
     ```sql
     CREATE TABLE Student (
         student_id NUMBER(5) PRIMARY KEY,
         student_name CHAR(20) UNIQUE,
         dept CHAR(10) NOT NULL,
         age NUMBER(2)
     );
     ```

2. **Add Column**:  
   - Add additional columns to a table after it has been created.  
   - **Example**:
     ```sql
     ALTER TABLE Student ADD grade VARCHAR2(5);
     ```

3. **Drop Column**:  
   - Remove an unnecessary column from a table.  
   - **Example**:
     ```sql
     ALTER TABLE Student DROP COLUMN grade;
     ```

4. **Rename Column**:  
   - Rename an existing column in a table.  
   - **Example**:
     ```sql
     ALTER TABLE Student RENAME COLUMN city TO address;
     ```

5. **Drop Table**:  
   - Delete the table entirely, including its structure and all stored data.  
   - **Example**:
     ```sql
     DROP TABLE Student;
     ```

6. **Truncate Table**:  
   - Clear all rows in a table but keep the structure intact for future use.  
   - **Example**:
     ```sql
     TRUNCATE TABLE Student;
     ```

---

Made with 🫶🏻 by Franz Kingstein
