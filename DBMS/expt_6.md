# Ex-6: Procedures and Functions

✅ **Objective**:  
Learn and implement PL/SQL procedures and functions for data retrieval, calculations, and exception handling in database operations.

---
## **Concepts**

### **1. Procedure**
- A stored block of SQL code that performs specific tasks like retrieving, updating, or manipulating data.  

- **Syntax to Create a Procedure**:  
    ```sql
    CREATE OR REPLACE PROCEDURE procedure_name (param1 IN datatype, param2 OUT datatype) AS
    BEGIN
        -- SQL statements
        EXCEPTION
            WHEN NO_DATA_FOUND THEN DBMS_OUTPUT.PUT_LINE('No data found.');
            WHEN OTHERS THEN DBMS_OUTPUT.PUT_LINE('An error occurred.');
    END;
    / 
    ```

- **How to Call a Procedure**:  
    ```sql
    DECLARE
        output_variable datatype;
    BEGIN
        procedure_name(input_value, output_variable);
        DBMS_OUTPUT.PUT_LINE('Output: ' || output_variable);
    END;
    /
    ```

---

### **2. Function**
- A stored block that returns a value based on input and operations performed.  

- **Syntax to Create a Function**:  
    ```sql
    CREATE OR REPLACE FUNCTION function_name (param1 IN datatype) RETURN datatype AS
        result_variable datatype;
    BEGIN
        -- SQL statements
        RETURN result_variable;
        EXCEPTION
            WHEN NO_DATA_FOUND THEN RETURN NULL;
    END;
    /
    ```

- **How to Call a Function**:  
    ```sql
    DECLARE
        result datatype;
    BEGIN
        result := function_name(input_value);
        DBMS_OUTPUT.PUT_LINE('Result: ' || result);
    END;
    /
    ```

---

## **Unique Solution Questions**

✅ **1. Fetch Salary and Assign Grade**  
**Task**: Determine the grade of an employee based on their salary.  
**SQL Code**:  
```sql
DECLARE
    v_salary NUMBER;
    v_grade CHAR(1);
BEGIN
    -- Fetch salary for employee 'ANIL'
    SELECT salary INTO v_salary FROM Employee_URK23AI1112 WHERE name = 'ANIL';

    -- Determine grade based on salary
    IF v_salary < 1000 THEN
        v_grade := 'A';
    ELSIF v_salary < 2000 THEN
        v_grade := 'B';
    ELSIF v_salary < 3000 THEN
        v_grade := 'C';
    ELSIF v_salary < 4000 THEN
        v_grade := 'D';
    ELSE
        v_grade := 'E';
    END IF;

    -- Display salary and grade
    DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary || ' | Grade: ' || v_grade);
END;
/
```

**Output**:
```plaintext
Salary: 2500 | Grade: C
```

---

✅ **2. Procedure to Get Course Name**  
**Task**: Retrieve the course name based on its course code.  
**SQL Code**:  
```sql
CREATE OR REPLACE PROCEDURE Get_CourseName_URK23AI1112 (
    p_coursecode IN NUMBER,
    p_coursename OUT VARCHAR2
) AS
BEGIN
    SELECT coursename INTO p_coursename FROM Course_URK23AI1112 WHERE coursecode = p_coursecode;
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            p_coursename := 'Course Not Found';
        WHEN OTHERS THEN
            p_coursename := 'Error Occurred';
END;
/
```

**Calling the Procedure**:  
```sql
DECLARE
    v_coursename VARCHAR2(100);
BEGIN
    Get_CourseName_URK23AI1112(10, v_coursename);
    DBMS_OUTPUT.PUT_LINE('Course Name: ' || v_coursename);
END;
/
```

---

✅ **3. Procedure for Exception Handling (Course Name)**  
**Task**: Handle exceptions when retrieving course names.  
**SQL Code**:  
```sql
CREATE OR REPLACE PROCEDURE Get_CourseName_Exception_URK23AI1112 (
    p_coursecode IN NUMBER
) AS
    v_coursename VARCHAR2(100);
BEGIN
    SELECT coursename INTO v_coursename FROM Course_URK23AI1112 WHERE coursecode = p_coursecode;
    DBMS_OUTPUT.PUT_LINE('Course Name: ' || v_coursename);
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
            DBMS_OUTPUT.PUT_LINE('Error: Course Name is not available.');
END;
/
```

**Calling the Procedure**:  
```sql
BEGIN
    Get_CourseName_Exception_URK23AI1112(99); -- Use a test course code
END;
/
```

---

✅ **4. Function to Calculate Total Amount Collected**  
**Task**: Compute the total amount collected from the `FeesPaid` table.  
**SQL Code**:  
```sql
CREATE OR REPLACE FUNCTION Total_Amount_Collected_URK23AI1112 RETURN NUMBER AS
    v_total_amount NUMBER;
BEGIN
    SELECT SUM(amount) INTO v_total_amount FROM FeesPaid_URK23AI1112;
    RETURN v_total_amount;
END;
/
```

**Calling the Function**:  
```sql
DECLARE
    v_total NUMBER;
BEGIN
    v_total := Total_Amount_Collected_URK23AI1112;
    DBMS_OUTPUT.PUT_LINE('Total Amount Collected: ' || v_total);
END;
/
```

---

✅ **5. Function to Calculate Fees Paid by a Student**  
**Task**: Compute the total fees paid by a specific student.  
**SQL Code**:  
```sql
CREATE OR REPLACE FUNCTION Total_Fees_Paid_URK23AI1112 (
    p_student_name IN VARCHAR2
) RETURN NUMBER AS
    v_total_fees NUMBER;
BEGIN
    SELECT SUM(amount) INTO v_total_fees FROM FeesPaid_URK23AI1112 WHERE rollno = (SELECT rollno FROM Student_URK23AI1112 WHERE name = p_student_name);
    IF v_total_fees IS NULL THEN
        RETURN 0;
    ELSE
        RETURN v_total_fees;
    END IF;
END;
/
```

**Calling the Function**:  
```sql
DECLARE
    v_total_fees NUMBER;
BEGIN
    v_total_fees := Total_Fees_Paid_URK23AI1112('John Doe');
    DBMS_OUTPUT.PUT_LINE('Total Fees Paid: ' || v_total_fees);
END;
/
```

---

## **CheatSheet**

| **Feature**               | **Purpose**                                     | **Example Syntax**                                                                 |
|----------------------------|------------------------------------------------|------------------------------------------------------------------------------------|
| **Procedure**              | Perform tasks without returning values         | `CREATE OR REPLACE PROCEDURE procedure_name AS BEGIN ... END;`                    |
| **Function**               | Perform tasks and return values                | `CREATE OR REPLACE FUNCTION function_name RETURN datatype AS BEGIN ... END;`       |
| **Handling Exceptions**    | Manage errors during execution                 | `EXCEPTION WHEN NO_DATA_FOUND THEN ... WHEN OTHERS THEN ...;`                      |
| **DBMS_OUTPUT.PUT_LINE**   | Print messages to the console                  | `DBMS_OUTPUT.PUT_LINE('Message');`                                                |
| **DECLARE**                | Define variables for procedures/functions      | `DECLARE variable_name datatype;`                                                 |

---

✅ **Conclusion**:  
Successfully demonstrated the implementation of PL/SQL procedures and functions to retrieve data, calculate values, and handle exceptions effectively.

---
Made with 🫶🏻 by Franz Kingstein
