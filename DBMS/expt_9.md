---

# **Ex-9: CRUD Operations Using MongoDB**

✅ **Objective**:  
To perform **CRUD operations** (Create, Read, Update, Delete) using MongoDB and understand how MongoDB stores and retrieves data dynamically.

---

## **Concepts**

### **MongoDB**  
**Concept**: MongoDB is a NoSQL database that stores data in a document-oriented format instead of traditional tables and rows.  

### **Key Features**  
1. **Document-Oriented**:  
   - Data is stored as **JSON-like BSON (Binary JSON)** documents.  
   - Each document is a collection of **key-value pairs**, enabling flexible schema design.  

2. **Schema-Less**:  
   - No need for predefined schemas, allowing documents in a collection to have diverse structures.  

3. **Scalability and Performance**:  
   - Supports **horizontal scaling** using sharding.  
   - Offers fast read/write operations with **indexing**.  

4. **Replication and Availability**:  
   - Uses replica sets for redundancy and failover protection.  

---

## **CRUD Operations**

### **Create**  
- Insert single or multiple documents into a MongoDB collection.  

**Java Code**:  
```java
Document user = new Document("name", "Franz")
                    .append("email", "franzkingstein@gmail.com")
                    .append("age", 25);
collection.insertOne(user); // Inserts a single document
System.out.println("User inserted successfully");

Document user1 = new Document("name", "Joel")
                    .append("email", "joelking@gmail.com")
                    .append("age", 30);
Document user2 = new Document("name", "Abunesh")
                    .append("email", "abunesh@gmail.com")
                    .append("age", 28);
collection.insertMany(Arrays.asList(user1, user2)); // Inserts multiple documents
System.out.println("Users inserted successfully");
```

---

### **Read**  
- Retrieve and display documents stored in a collection.  

**Java Code**:  
```java
FindIterable<Document> users = collection.find(); // Fetch all documents
for (Document user : users) {
    System.out.println(user.toJson());
}
```

---

### **Update**  
- Modify existing documents in a collection based on a filter condition.  

**Java Code**:  
```java
collection.updateOne(Filters.eq("name", "Franz"), Updates.set("age", 12)); // Updates age to 12
System.out.println("User updated successfully");
```

---

### **Delete**  
- Remove documents from the collection based on a filter condition.  

**Java Code**:  
```java
collection.deleteOne(Filters.eq("name", "Joel")); // Deletes the document with name "Joel"
System.out.println("User deleted successfully");
```

---

## **Full Java Program for CRUD Operations**

**Java Code**:  
```java
import com.mongodb.client.MongoClient;
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoDatabase;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.model.Filters;
import com.mongodb.client.model.Updates;
import org.bson.Document;

public class App {
    public static void main(String[] args) {
        String uri = "mongodb+srv://myAtlasDBUser:Joes_2009@myatlasclusteredu.mongodb.net/?retryWrites=true&w=majority&appName=myAtlasClusterEDU";

        try (MongoClient mongoClient = MongoClients.create(uri)) {
            MongoDatabase database = mongoClient.getDatabase("test");
            MongoCollection<Document> collection = database.getCollection("user");

            // Create: Insert Documents
            Document user = new Document("name", "Franz").append("email", "franzkingstein@gmail.com").append("age", 25);
            collection.insertOne(user);

            // Read: Retrieve Documents
            for (Document iuser : collection.find()) {
                System.out.println(iuser.toJson());
            }

            // Update: Modify Document
            collection.updateOne(Filters.eq("name", "Franz"), Updates.set("age", 12));

            // Delete: Remove Document
            collection.deleteOne(Filters.eq("name", "Joel"));
        } catch (Exception e) {
            System.out.println("Error occurred: " + e.getMessage());
        }
    }
}
```

---

## **CheatSheet**

| **Operation** | **Purpose**                    | **Java Code Example**                                     |
|---------------|--------------------------------|----------------------------------------------------------|
| **Create**    | Insert new documents           | `collection.insertOne(doc);` / `collection.insertMany(list);` |
| **Read**      | Retrieve documents             | `collection.find()`                                      |
| **Update**    | Modify an existing document    | `collection.updateOne(Filters.eq(field, value), Updates.set(field, newValue));` |
| **Delete**    | Remove a document              | `collection.deleteOne(Filters.eq(field, value));`        |

---

✅ **Result**:  
CRUD operations were performed successfully using MongoDB.

---
