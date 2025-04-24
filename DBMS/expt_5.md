---

# **Ex-5: Triggers**

✅ **Objective**:  
Demonstrate the working of Triggers in automating database operations, enforcing rules, and maintaining data consistency.

---

## **General Syntax for Triggers**

### **1. Create Trigger**
**Purpose**: Define a trigger that executes a procedure upon an event (INSERT, UPDATE, DELETE).  
**Syntax**:  
```sql
CREATE OR REPLACE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT OR UPDATE OR DELETE} ON table_name
FOR EACH ROW
BEGIN
    -- Trigger logic here
END;
/
```

---

### **2. Validation Using RAISE_APPLICATION_ERROR**
**Purpose**: Prevent invalid data manipulation by displaying a custom error message.  
**Syntax**:  
```sql
IF condition THEN
    RAISE_APPLICATION_ERROR(-20001, 'Custom error message');
END IF;
```

---

## **Trigger Examples Implemented**

### **1. Validate Course Code**
**Ensure `coursecode` is a two-digit number (10-99).**  
```sql
CREATE OR REPLACE TRIGGER validate_course_code
BEFORE INSERT ON Course
FOR EACH ROW
BEGIN
    IF :NEW.coursecode < 10 OR :NEW.coursecode > 99 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Invalid course code! It must be between 10 and 99.');
    END IF;
END;
/
```

---

### **2. Restrict DML Operations for 'student1'**
**Prevent `INSERT`, `UPDATE`, or `DELETE` by the user `student1`.**  
```sql
CREATE OR REPLACE TRIGGER restrict_student1_dml
BEFORE INSERT OR UPDATE OR DELETE ON Enquiry
FOR EACH ROW
BEGIN
    IF USER = 'STUDENT1' THEN
        RAISE_APPLICATION_ERROR(-20002, 'DML operations are not allowed for student1');
    END IF;
END;
/
```

---

### **3. Restrict Fees Below 10,000**
**Block `INSERT` operation if `amount` is less than 10,000 in the `FeesPaid` table.**  
```sql
CREATE OR REPLACE TRIGGER restrict_low_fees
BEFORE INSERT ON FeesPaid
FOR EACH ROW
BEGIN
    IF :NEW.amount < 10000 THEN
        RAISE_APPLICATION_ERROR(-20003, 'Amount must be at least 10,000');
    END IF;
END;
/
```

---

### **4. Restrict Enquiry Dates After 25-Aug-2017**
**Prevent `INSERT` operation if `enquirydate` is beyond 25-Aug-2017 in the `Enquiry` table.**  
```sql
CREATE OR REPLACE TRIGGER restrict_enquiry_date
BEFORE INSERT ON Enquiry
FOR EACH ROW
BEGIN
    IF :NEW.enquirydate > TO_DATE('25-AUG-2017', 'DD-MON-YYYY') THEN
        RAISE_APPLICATION_ERROR(-20004, 'Enquiry date cannot be after 25-Aug-2017');
    END IF;
END;
/
```

---

### **5. Prevent Incorrect Updates**
**Block updates in `Enquiry` table where `OLD.name` is modified to a new value.**  
```sql
CREATE OR REPLACE TRIGGER prevent_name_update
BEFORE UPDATE ON Enquiry
FOR EACH ROW
BEGIN
    IF :OLD.name <> :NEW.name THEN
        RAISE_APPLICATION_ERROR(-20005, 'Name cannot be modified');
    END IF;
END;
/
```

---

### **6. Restrict Fees if Average Exceeds 50,000**
**Block `INSERT` in `FeesPaid` table if the average `amount` exceeds 50,000.**  
```sql
CREATE OR REPLACE TRIGGER restrict_high_avg_fees
BEFORE INSERT ON FeesPaid
FOR EACH ROW
DECLARE
    avg_fees NUMBER;
BEGIN
    SELECT AVG(amount) INTO avg_fees FROM FeesPaid;
    IF avg_fees > 50000 THEN
        RAISE_APPLICATION_ERROR(-20006, 'Cannot insert, average fees exceed 50,000');
    END IF;
END;
/
```

---

### **7. Restrict Negative Salaries**
**Prevent negative values in the `salary` column during `INSERT` or `UPDATE` operations.**  
```sql
CREATE OR REPLACE TRIGGER restrict_negative_salary
BEFORE INSERT OR UPDATE ON Employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 0 THEN
        RAISE_APPLICATION_ERROR(-20007, 'Salary cannot be negative');
    END IF;
END;
/
```

---

### **8. Log Changes in the `Course` Table**
**Audit updates in the `Course` table by logging changes into a separate audit table.**  
```sql
CREATE OR REPLACE TRIGGER log_course_updates
AFTER UPDATE ON Course
FOR EACH ROW
BEGIN
    INSERT INTO CourseAudit(coursecode, updated_by, timestamp)
    VALUES (:OLD.coursecode, USER, SYSDATE);
END;
/
```

---

### **9. Log Enquiry Insertions**
**Track every `INSERT` operation in the `Enquiry` table by logging the action.**  
```sql
CREATE OR REPLACE TRIGGER log_enquiry_insertions
AFTER INSERT ON Enquiry
FOR EACH ROW
BEGIN
    INSERT INTO EnquiryLog(enquirydate, user, action)
    VALUES (:NEW.enquirydate, USER, 'INSERT');
END;
/
```

---

## **CheatSheet for Triggers**

| **Trigger Type**               | **Purpose**                                                      | **Syntax**                                                                 |
|--------------------------------|------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **BEFORE INSERT Trigger**      | Validates or blocks data before it is inserted into a table      | `BEFORE INSERT ON table_name FOR EACH ROW BEGIN ... END; /`                 |
| **BEFORE UPDATE Trigger**      | Validates or blocks changes during updates                      | `BEFORE UPDATE ON table_name FOR EACH ROW BEGIN ... END; /`                 |
| **BEFORE DELETE Trigger**      | Blocks or manages delete operations                             | `BEFORE DELETE ON table_name FOR EACH ROW BEGIN ... END; /`                 |
| **AFTER UPDATE Trigger**       | Logs or audits changes after data modification                  | `AFTER UPDATE ON table_name FOR EACH ROW BEGIN ... END; /`                  |
| **RAISE_APPLICATION_ERROR**    | Stops the operation and displays an error message               | `RAISE_APPLICATION_ERROR(-error_code, 'Error message');`                   |

---

✅ **Conclusion**:  
Successfully demonstrated trigger implementations for automating database actions, enforcing rules, logging events, and maintaining data consistency.

--- 
