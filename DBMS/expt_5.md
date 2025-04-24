Here’s the markdown for **Ex-5: Triggers**, formatted exactly as the previous template for clarity and simplicity:

---

# **Ex-5: Triggers**

✅ **1. Create a table for Courses**  
**Concept**: A table is used to store data in an organized way. The `Course` table stores details about different courses.  

**SQL Syntax**:  
```sql
CREATE TABLE Course (
    coursecode INT PRIMARY KEY,
    coursename VARCHAR(255),
    syllabus TEXT,
    lastno INT
);
```

**Explanation**:  
- `coursecode`: Unique identifier for a course (Primary Key).  
- `coursename`: Name of the course.  
- `syllabus`: Text information about the course contents.  
- `lastno`: Some associated numerical value for a course.

---

✅ **2. Trigger to Validate Course Code**  
**Concept**: Before inserting into the `Course` table, check that `coursecode` is a two-digit number between 10 and 99.

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

**Explanation**:  
- **Trigger**: Runs automatically before inserting a row into the `Course` table.  
- If `coursecode` is outside the range (10–99), it stops the insertion with an error message.

---

✅ **3. Restrict DML for 'student1'**  
**Concept**: Prevent any data operations (**INSERT**, **UPDATE**, **DELETE**) on the `Enquiry` table by the user `student1`.

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

**Explanation**:  
- **Trigger**: Automatically blocks data operations by `student1` with an error message.  
- `current_user`: The username attempting the operation.

---

✅ **4. Restrict Fees Below 10,000**  
**Concept**: Prevent inserting payments in the `FeesPaid` table where the `amount` is less than 10,000.

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

**Explanation**:  
- **Trigger**: Checks the `amount` before adding payments.  
- If the `amount` is less than 10,000, the insertion is blocked with an error.

---

✅ **5. Restrict Enquiry Dates After 25-Aug-2017**  
**Concept**: Do not allow inserting enquiries with a date after 25-Aug-2017.

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

**Explanation**:  
- **Trigger**: Activates before adding enquiries.  
- If the date exceeds 25-Aug-2017, insertion is blocked with a message.

---

✅ **6. Prevent Incorrect Updates**  
**Concept**: Block updates in the `Enquiry` table if the `name` column does not match the previous value.

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

**Explanation**:  
- **Trigger**: Runs before updating a row in the `Enquiry` table.  
- Compares `OLD.name` (existing name) and `NEW.name` (new name) to ensure consistency.

---

✅ **7. Restrict Fees if Average Exceeds 50,000**  
**Concept**: Block inserting fees in the `FeesPaid` table if the average fee exceeds 50,000.

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

**Explanation**:  
- **Trigger**: Runs before adding payments to the `FeesPaid` table.  
- Checks the average of all fees paid so far. If it’s above 50,000, insertion is blocked.

---

## **CheatSheet**

| **Trigger Type**               | **Purpose**                                                      | **Example Syntax**                                                                 |
|--------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **BEFORE INSERT Trigger**      | Validate or block data before inserting                         | `BEFORE INSERT ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **BEFORE UPDATE Trigger**      | Validate or block updates to a table                           | `BEFORE UPDATE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **BEFORE DELETE Trigger**      | Block or handle delete operations                              | `BEFORE DELETE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name();`       |
| **RAISE EXCEPTION**            | Stop action and display custom error message                   | `RAISE EXCEPTION 'Error message';`                                                |
| **Validation Function**        | Use logic to validate data before completing an operation       | `IF NEW.column_name > value THEN ... RETURN NEW;`                                  |
| **Average Check**              | Validate data based on calculations (e.g., average fees)       | `SELECT AVG(column_name) INTO variable_name FROM table_name;`                      |

---

✅ **Conclusion**:  
Successfully demonstrated the working of database triggers to automate checks, maintain data integrity, and enforce rules.

---

Let me know if you need further clarification or refinements! 😊
