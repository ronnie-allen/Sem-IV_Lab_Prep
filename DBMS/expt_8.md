# **Ex-8: JDBC**

✅ **Objective**:  
Develop a Java application using JDBC (Java Database Connectivity) and execute database queries effectively.

---

## **Concepts**

### **JDBC**  
**Concept**: JDBC is an API for Java that allows applications to interact with databases. It provides methods to establish connections, execute SQL queries, and manage results.  

---

### **Steps for JDBC Connectivity**

✅ **1. Load the Database Driver**  
**Concept**: Load the required driver class to connect Java with a specific database.  

**Syntax**:  
```java
Class.forName("org.postgresql.Driver");
```

---

✅ **2. Establish Connection**  
**Concept**: Use the `DriverManager` class to create a connection to the database with the proper credentials.  

**Syntax**:  
```java
Connection con = DriverManager.getConnection("jdbc:postgresql://localhost:5432/postgres", "username", "password");
```

---

✅ **3. Execute SQL Queries**  
**Concept**: Execute queries like SELECT, INSERT, UPDATE using `Statement` or `PreparedStatement` objects.  

**Syntax**:  
```java
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM table_name");
```

---

✅ **4. Handle Exceptions**  
**Concept**: Handle errors like missing drivers (`ClassNotFoundException`) or invalid database credentials (`SQLException`).  

**Syntax**:  
```java
catch (ClassNotFoundException e) {
    e.printStackTrace();
} catch (SQLException e) {
    e.printStackTrace();
}
```

---

## **Solution Example**

### **Code Example**  
**Task**: Create a Java program to connect to a PostgreSQL database and verify the connection.  

**Java Code**:  
```java
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Connection;

public class JdbcTrying {
    public static void main(String[] args) {
        try {
            // Load the driver
            Class.forName("org.postgresql.Driver");

            // Establish connection
            Connection con = DriverManager.getConnection("jdbc:postgresql://localhost:5432/postgres", "postgres", "Joes@2009");
            System.out.println("Connection created");
        } catch (ClassNotFoundException e) {
            e.printStackTrace(); // Handles missing driver class
        } catch (SQLException e) {
            e.printStackTrace(); // Handles SQL connection issues
        }
    }
}
```

---

### **Output**  
```plaintext
Connection created
```

---

## **CheatSheet**

| **JDBC Step**              | **Purpose**                                    | **Syntax**                                                                  |
|-----------------------------|------------------------------------------------|-----------------------------------------------------------------------------|
| **Load Driver**             | Load database-specific driver                  | `Class.forName("org.postgresql.Driver");`                                   |
| **Establish Connection**    | Connect to the database using credentials      | `DriverManager.getConnection("jdbc:postgresql://localhost:5432/db", "user", "pass");` |
| **Execute Queries**         | Perform SELECT, INSERT, UPDATE operations      | `stmt.executeQuery("SELECT * FROM table_name");`                           |
| **Handle Exceptions**       | Handle JDBC-related errors                     | `catch (ClassNotFoundException e) { e.printStackTrace(); }`                |

---

✅ **Conclusion**:  
The working of JDBC connectivity was demonstrated successfully, and queries were executed without errors.

---
Made with 🫶🏻 by Franz Kingstein
