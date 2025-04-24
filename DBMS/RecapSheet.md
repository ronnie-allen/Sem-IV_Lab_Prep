# Common Cheat Sheet for All 10 Experiments

This cheat sheet summarizes the key concepts, syntax, and operations across all 10 experiments for quick reference.

---

## **Experiment 1: DDL and DML Commands**

Here’s an improved, more detailed and clear version of the CheatSheet for **DDL Commands**:

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

## **Experiment 2: SQL DDL and TCL Commands**

| **Command**         | **Purpose**                                   | **Syntax**                                      |
|---------------------|-----------------------------------------------|------------------------------------------------|
| **CREATE TABLE**    | Define a new table                            | `CREATE TABLE table_name (...);`              |
| **ALTER TABLE**     | Add, modify, or remove a column               | `ALTER TABLE table_name ADD column_name datatype;` |
| **DROP TABLE**      | Permanently delete a table                    | `DROP TABLE table_name;`                       |
| **COMMIT**          | Save all changes                              | `COMMIT;`                                      |
| **ROLLBACK**        | Undo all uncommitted changes                  | `ROLLBACK;`                                    |

---

## **Experiment 3: SQL Set Operations**

| **Operation**       | **Purpose**                                   | **Syntax**                                      |
|---------------------|-----------------------------------------------|------------------------------------------------|
| **UNION**           | Combine unique rows from multiple tables      | `SELECT ... UNION SELECT ...;`                |
| **INTERSECT**       | Return common rows                            | `SELECT ... INTERSECT SELECT ...;`            |
| **EXCEPT**          | Return rows in one table but not the other    | `SELECT ... EXCEPT SELECT ...;`               |

---

## **Experiment 4: SQL JOIN Operations**

| **Join Type**       | **Purpose**                                   | **Syntax**                                      |
|---------------------|-----------------------------------------------|------------------------------------------------|
| **INNER JOIN**      | Return rows with matching values              | `SELECT ... INNER JOIN ... ON condition;`      |
| **LEFT JOIN**       | Include all rows from left table              | `SELECT ... LEFT JOIN ... ON condition;`       |
| **CROSS JOIN**      | Return Cartesian product of two tables        | `SELECT ... CROSS JOIN ...;`                  |

---



## **Experiment 5: Triggers**

| **Trigger Type**     | **Purpose**                                  | **Example Syntax**                                                                 |
|----------------------|----------------------------------------------|------------------------------------------------------------------------------------|
| **BEFORE INSERT Trigger** | Validates or blocks data before insertion into a table | ```sql BEFORE INSERT ON table_name FOR EACH ROW EXECUTE FUNCTION function_name(); ``` |
| **BEFORE UPDATE Trigger** | Validates or blocks changes during updates | ```sql BEFORE UPDATE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name(); ``` |
| **BEFORE DELETE Trigger** | Blocks deletion or handles specific scenarios | ```sql BEFORE DELETE ON table_name FOR EACH ROW EXECUTE FUNCTION function_name(); ``` |
| **RAISE EXCEPTION**      | Throws custom error messages for invalid operations | ```sql RAISE EXCEPTION 'Error message'; ```                                        |
| **Validation Example**   | Ensures data integrity (e.g., course code validation) | ```sql IF NEW.coursecode < 10 OR NEW.coursecode > 99 THEN RAISE EXCEPTION 'Invalid course code!'; ``` |

---

## **Experiment 6: Procedures and Functions**

| **Feature**          | **Purpose**                              | **Syntax**                                                                    |
|----------------------|------------------------------------------|-------------------------------------------------------------------------------|
| **Procedure**         | Executes tasks without returning values | ```sql CREATE OR REPLACE PROCEDURE procedure_name (param IN datatype, param OUT datatype) AS BEGIN ... END; ``` |
| **Function**          | Executes tasks and returns a value      | ```sql CREATE OR REPLACE FUNCTION function_name (param IN datatype) RETURN datatype AS BEGIN RETURN value; END; ``` |
| **Handling Exceptions** | Manages errors during procedure/function execution | ```sql EXCEPTION WHEN NO_DATA_FOUND THEN DBMS_OUTPUT.PUT_LINE('No data found.'); WHEN OTHERS THEN DBMS_OUTPUT.PUT_LINE('An error occurred.'); ``` |
| **DBMS_OUTPUT.PUT_LINE** | Prints debugging or informational messages | ```sql DBMS_OUTPUT.PUT_LINE('Your Message'); ```                              |
| **Variables**          | Declare variables for operations       | ```sql DECLARE variable_name datatype; ```                                    |

---
## **Experiment 7: Aggregate and Built-in Functions**

| **Function Type**    | **Purpose**                                   | **Syntax**                                      |
|----------------------|-----------------------------------------------|------------------------------------------------|
| **SUM**              | Calculate total value                        | `SELECT SUM(column_name) FROM table_name;`     |
| **COUNT**            | Count number of rows                         | `SELECT COUNT(*) FROM table_name;`            |
| **ROUND**            | Round a number                               | `SELECT ROUND(number, decimal_places);`       |
| **SUBSTR**           | Extract a substring                          | `SELECT SUBSTR(column, start, length);`       |

---

## **Experiment 8: JDBC**

| **Step**              | **Purpose**                                  | **Java Code**                                   |
|-----------------------|----------------------------------------------|------------------------------------------------|
| **Load Driver**        | Load database-specific driver                | `Class.forName("org.postgresql.Driver");`      |
| **Create Connection**  | Connect to the database                     | `DriverManager.getConnection(...);`           |
| **Execute Queries**    | Run SQL commands                            | `stmt.executeQuery("SELECT ...");`            |

---

## **Experiment 9: MongoDB CRUD**

| **Operation**         | **Purpose**                                   | **Java Code**                                   |
|-----------------------|-----------------------------------------------|------------------------------------------------|
| **Create**            | Insert a document                            | `collection.insertOne(document);`             |
| **Read**              | Fetch documents                              | `collection.find();`                          |
| **Update**            | Modify existing document                     | `collection.updateOne(Filters.eq(...), Updates.set(...));` |
| **Delete**            | Remove a document                            | `collection.deleteOne(Filters.eq(...));`      |

---

## **Experiment 10: Normalization**

| **Normal Form**       | **Condition**                                 | **Description**                                |
|-----------------------|-----------------------------------------------|------------------------------------------------|
| **1NF**               | Atomic values only                           | Remove multi-valued attributes.               |
| **2NF**               | Full functional dependency                   | Eliminate partial dependencies.               |
| **3NF**               | Remove transitive dependencies               | Ensure no dependency on non-primary key.      |
| **BCNF**              | Superkey requirement                         | Ensure all functional dependencies are with superkeys. |
| **4NF & 5NF**         | Remove multi-valued and join dependencies     | Decompose tables while retaining data.        |

---

This cheat sheet compiles the critical commands and concepts across all 10 experiments for quick reference and efficient learning.
