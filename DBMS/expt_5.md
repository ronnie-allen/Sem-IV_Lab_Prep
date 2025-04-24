# **Ex-5: Triggers**

✅ **Objective**:  
Demonstrate the working of Triggers to automate database operations, enforce rules, and maintain data integrity.

---

## **Trigger Scenarios**

### **1. Create a Table for Courses**
- **Purpose**: Creating a table to store data about courses.  
**SQL Syntax**:  
```sql
CREATE TABLE Course (
    coursecode INT PRIMARY KEY,
    coursename VARCHAR(255),
    syllabus TEXT,
    lastno INT
);
```

---

### **2. Trigger to Validate Course Code**
- **Purpose**: Ensure course code is a two-digit number between 10 and 99.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION check_course_code()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.coursecode < 10 OR NEW.coursecode > 99 THEN
        RAISE EXCEPTION 'Invalid course code! It must be between 10 and 99.';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER course_code_trigger
BEFORE INSERT ON Course
FOR EACH ROW
EXECUTE FUNCTION check_course_code();
```

---

### **3. Restrict DML for 'student1'**
- **Purpose**: Prevent `INSERT`, `UPDATE`, or `DELETE` operations on the `Enquiry` table by the user `student1`.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION restrict_student1()
RETURNS TRIGGER AS $$
BEGIN
    IF current_user = 'student1' THEN
        RAISE EXCEPTION 'DML operations are not allowed for student1';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER restrict_student1_trigger
BEFORE INSERT OR UPDATE OR DELETE ON Enquiry
FOR EACH ROW
EXECUTE FUNCTION restrict_student1();
```

---

### **4. Restrict Fees Below 10,000**
- **Purpose**: Prevent inserting fees in the `FeesPaid` table if the amount is less than 10,000.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION check_fees_amount()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.amount < 10000 THEN
        RAISE EXCEPTION 'Amount must be at least 10,000';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER fees_amount_trigger
BEFORE INSERT ON FeesPaid
FOR EACH ROW
EXECUTE FUNCTION check_fees_amount();
```

---

### **5. Restrict Enquiry Dates After 25-Aug-2017**
- **Purpose**: Do not allow inserting enquiries with a date after 25-Aug-2017.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION restrict_enquiry_date()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.enquirydate > '2017-08-25' THEN
        RAISE EXCEPTION 'Enquiry date cannot be after 25-Aug-17';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER enquiry_date_trigger
BEFORE INSERT ON Enquiry
FOR EACH ROW
EXECUTE FUNCTION restrict_enquiry_date();
```

---

### **6. Prevent Incorrect Updates**
- **Purpose**: Ensure no updates in the `Enquiry` table change the value of the `name` column.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION prevent_wrong_update()
RETURNS TRIGGER AS $$
BEGIN
    IF OLD.name <> NEW.name THEN
        RAISE EXCEPTION 'Old value must match the existing value';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER prevent_update_trigger
BEFORE UPDATE ON Enquiry
FOR EACH ROW
EXECUTE FUNCTION prevent_wrong_update();
```

---

### **7. Restrict Fees if Average Exceeds 50,000**
- **Purpose**: Block inserting fees in the `FeesPaid` table if the average fee exceeds 50,000.  
**SQL Syntax**:  
```sql
CREATE OR REPLACE FUNCTION check_avg_fees()
RETURNS TRIGGER AS $$
DECLARE
    avg_fees DECIMAL(10,2);
BEGIN
    SELECT AVG(amount) INTO avg_fees FROM FeesPaid;
    IF avg_fees > 50000 THEN
        RAISE EXCEPTION 'Cannot insert, average fees exceed 50,000';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER avg_fees_trigger
BEFORE INSERT ON FeesPaid
FOR EACH ROW
EXECUTE FUNCTION check_avg_fees();
```

---

## **Unique Solution Questions**

✅ **1. Create a Trigger to Restrict Negative Salaries**  
**SQL**:  
```sql
CREATE OR REPLACE FUNCTION restrict_negative_salary()
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.salary < 0 THEN
        RAISE EXCEPTION 'Salary cannot be negative';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER salary_trigger
BEFORE INSERT OR UPDATE ON Employees
FOR EACH ROW
EXECUTE FUNCTION restrict_negative_salary();
```

---

✅ **2. Trigger to Audit Course Updates**  
**SQL**:  
```sql
CREATE OR REPLACE FUNCTION audit_course_updates()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO CourseAudit(coursecode, updated_by, timestamp)
    VALUES(OLD.coursecode, current_user, CURRENT_TIMESTAMP);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER audit_trigger
AFTER UPDATE ON Course
FOR EACH ROW
EXECUTE FUNCTION audit_course_updates();
```

---

✅ **3. Prevent Deletion of High Fees Records**  
**SQL**:  
```sql
CREATE OR REPLACE FUNCTION restrict_high_fees_deletion()
RETURNS TRIGGER AS $$
BEGIN
    IF OLD.amount > 50000 THEN
        RAISE EXCEPTION 'Cannot delete records with fees above 50,000';
    END IF;
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER restrict_deletion_trigger
BEFORE DELETE ON FeesPaid
FOR EACH ROW
EXECUTE FUNCTION restrict_high_fees_deletion();
```

---

✅ **4. Trigger to Log Enquiry Insertions**  
**SQL**:  
```sql
CREATE OR REPLACE FUNCTION log_enquiry_insertions()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO EnquiryLog(enquirydate, user, action)
    VALUES(NEW.enquirydate, current_user, 'INSERT');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER log_insertion_trigger
AFTER INSERT ON Enquiry
FOR EACH ROW
EXECUTE FUNCTION log_enquiry_insertions();
```

---

✅ **5. Restrict Updates to the Primary Key Column**  
**SQL**:  
```sql
CREATE OR REPLACE FUNCTION restrict_pk_update()
RETURNS TRIGGER AS $$
BEGIN
    IF OLD.id <> NEW.id THEN
        RAISE EXCEPTION 'Primary key updates are not allowed';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER restrict_pk_trigger
BEFORE UPDATE ON TableName
FOR EACH ROW
EXECUTE FUNCTION restrict_pk_update();
```

---

## **CheatSheet**

| **Trigger Type**               | **Purpose**                                                      | **Example Syntax**                                                                 |
|--------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **BEFORE INSERT Trigger**      | Validate or block data before inserting                         | `BEFORE INSERT ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **BEFORE UPDATE Trigger**      | Validate or block updates to a table                           | `BEFORE UPDATE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **BEFORE DELETE Trigger**      | Block or handle delete operations                              | `BEFORE DELETE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **RAISE EXCEPTION**            | Stop action and display custom error message                   | `RAISE EXCEPTION 'Error message';`                                                |
| **Validation Function**        | Use logic to validate data before completing an operation       | `IF NEW.column_name > value THEN ... RETURN NEW;`                                  |
| **Audit Function**             | Log changes into separate log tables                           | `INSERT INTO log_table(columns) VALUES(values);`                                   |

---

✅ **Conclusion**:  
Successfully demonstrated the working of database triggers to validate data, block invalid operations, and maintain data consistency.

---
