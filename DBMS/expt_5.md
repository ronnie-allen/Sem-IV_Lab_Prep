```markdown
# **Ex-5: Triggers**

✅ **Objective**:  
Demonstrate the working of Triggers in automating database operations, enforcing rules, and maintaining data consistency.

---

## **General Syntax for Triggers**

### **1. Create Trigger**
**Purpose**: Define a trigger that executes a function upon an event (INSERT, UPDATE, DELETE).  
**Syntax**:  
```sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE} ON table_name
FOR EACH ROW
EXECUTE FUNCTION function_name();
```

---

### **2. Create Trigger Function**
**Purpose**: Define the procedural code that executes when the trigger is activated.  
**Syntax**:  
```sql
CREATE OR REPLACE FUNCTION function_name()
RETURNS TRIGGER AS $$
BEGIN
    -- Trigger logic (e.g., validation, logging, exception handling)
    RETURN {NEW | OLD};
END;
$$ LANGUAGE plpgsql;
```

---

### **3. Validation Using RAISE EXCEPTION**
**Purpose**: Prevent invalid data manipulation by displaying a custom error message.  
**Syntax**:  
```sql
IF condition THEN
    RAISE EXCEPTION 'Custom error message';
END IF;
```

---

## **Trigger Functions Implemented**

### **1. Validate Course Code**
**Ensure `coursecode` is a two-digit number (10-99).**  
**Code**:  
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

### **2. Restrict DML Operations for 'student1'**
**Prevent `INSERT`, `UPDATE`, or `DELETE` by the user `student1`.**  
**Code**:  
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

### **3. Restrict Fees Below 10,000**
**Block `INSERT` operation if `amount` is less than 10,000 in the `FeesPaid` table.**  
**Code**:  
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

### **4. Restrict Enquiry Dates After 25-Aug-2017**
**Prevent `INSERT` operation if `enquirydate` is beyond 25-Aug-2017 in the `Enquiry` table.**  
**Code**:  
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

### **5. Prevent Incorrect Updates**
**Block updates in `Enquiry` table where `OLD.name` is modified to a new value.**  
**Code**:  
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

### **6. Restrict Fees if Average Exceeds 50,000**
**Block `INSERT` in `FeesPaid` table if the average `amount` exceeds 50,000.**  
**Code**:  
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

### **7. Restrict Negative Salaries**
**Prevent negative values in the `salary` column during `INSERT` or `UPDATE` operations.**  
**Code**:  
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

### **8. Log Changes in the `Course` Table**
**Audit updates in the `Course` table by logging changes into a separate audit table.**  
**Code**:  
```sql
CREATE OR REPLACE FUNCTION audit_course_updates()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO CourseAudit(coursecode, updated_by, timestamp)
    VALUES (OLD.coursecode, current_user, CURRENT_TIMESTAMP);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER audit_trigger
AFTER UPDATE ON Course
FOR EACH ROW
EXECUTE FUNCTION audit_course_updates();
```

---

### **9. Log Enquiry Insertions**
**Track every `INSERT` operation in the `Enquiry` table by logging the action.**  
**Code**:  
```sql
CREATE OR REPLACE FUNCTION log_enquiry_insertions()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO EnquiryLog(enquirydate, user, action)
    VALUES (NEW.enquirydate, current_user, 'INSERT');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER log_insertion_trigger
AFTER INSERT ON Enquiry
FOR EACH ROW
EXECUTE FUNCTION log_enquiry_insertions();
```

---

## **CheatSheet for Triggers**

| **Trigger Type**               | **Purpose**                                                      | **Syntax**                                                                 |
|--------------------------------|------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **BEFORE INSERT Trigger**      | Validates or blocks data before it is inserted into a table      | `BEFORE INSERT ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();` |
| **BEFORE UPDATE Trigger**      | Validates or blocks changes during updates                      | `BEFORE UPDATE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();` |
| **BEFORE DELETE Trigger**      | Blocks or manages delete operations                             | `BEFORE DELETE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();` |
| **AFTER UPDATE Trigger**       | Logs or audits changes after data modification                  | `AFTER UPDATE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();` |
| **RAISE EXCEPTION**            | Stops the operation and displays an error message               | `RAISE EXCEPTION 'Error message';`                                          |

---

✅ **Conclusion**:  
Successfully demonstrated trigger implementations for automating database actions, enforcing rules, logging events, and maintaining data consistency.

---

