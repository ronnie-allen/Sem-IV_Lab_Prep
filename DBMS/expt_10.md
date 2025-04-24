---

# **Ex-10: Normalization and Denormalization**

✅ **Objective**:  
Normalize tables for a given database application and learn the concepts behind database normalization and denormalization.

---

## **Concepts**

### **Database Normalization**  
**Concept**:  
Normalization is a technique to optimize the design of a database by reducing redundancy and avoiding anomalies during insertion, deletion, and updating.  

### **Types of Normalization**  
1. **First Normal Form (1NF)**:  
   - Attributes must have atomic (single) values.  
   - Remove multi-valued or composite attributes.  

2. **Second Normal Form (2NF)**:  
   - Table must be in 1NF.  
   - Every non-key attribute must depend only on the primary key.  

3. **Third Normal Form (3NF)**:  
   - Table must be in 2NF.  
   - No transitive dependencies (non-key attributes depending on other non-key attributes).  

4. **Boyce-Codd Normal Form (BCNF)**:  
   - Table must be in 3NF.  
   - No functional dependency violations (where non-superkey attributes functionally depend on each other).  

5. **Fourth and Fifth Normal Form (4NF, 5NF)**:  
   - 4NF ensures no multi-valued dependencies.  
   - 5NF ensures no join dependencies, and decomposition into smaller tables is lossless.  

---

## **Examples of Normalization**

### **Example 1: 1NF**  
**Task**: Convert a table with multi-valued attributes into 1NF.  

**Table Before Normalization**:
| Instructor Name | Course Code       |
|-----------------|-------------------|
| Prof. George    | CS101, CS154      |
| Prof. Atkins    | CS152             |

**Table After Normalization**:  
| Instructor Name | Course Code |
|-----------------|-------------|
| Prof. George    | CS101       |
| Prof. George    | CS154       |
| Prof. Atkins    | CS152       |

---

### **Example 2: 2NF**  
**Task**: Convert a table from 1NF to 2NF by breaking it into two tables.  

**Table Before Normalization**:  
| Student Name | Course Code |
|--------------|-------------|
| Rahul        | CS152       |
| Rajat        | CS101       |
| Raman        | CS101       |
| Rahul        | CS154       |

**Tables After Normalization**:

#### Students Table:  
| Student Name | Enrolment Number |
|--------------|------------------|
| Rahul        | 1                |
| Rajat        | 2                |
| Raman        | 3                |

#### Courses Table:  
| Course Code | Enrolment Number |
|-------------|------------------|
| CS152       | 1                |
| CS101       | 2                |
| CS101       | 3                |
| CS154       | 1                |

---

### **Example 3: 3NF**  
**Task**: Remove transitive dependencies from a table by splitting it into two tables.

**Table Before Normalization**:  
| Course Code | Venue           | Instructor Name | Department            |
|-------------|-----------------|-----------------|-----------------------|
| MA214       | Lecture Hall 18 | Prof. Ronald    | Mathematics Department|
| ME112       | Auditorium      | Prof. John      | Electronics Department|

**Tables After Normalization**:

#### Courses Table:  
| Course Code | Venue           | Instructor ID |
|-------------|-----------------|---------------|
| MA214       | Lecture Hall 18 | 1             |
| ME112       | Auditorium      | 2             |

#### Instructors Table:  
| Instructor ID | Instructor Name | Department             |
|---------------|-----------------|------------------------|
| 1             | Prof. Ronald    | Mathematics Department |
| 2             | Prof. John      | Electronics Department |

---

## **Additional Questions**

### **Normalize to 3NF**  
#### Input Table:
| SID | CID  | S_name | C_name     | Grade | Faculty | F_phone |
|-----|------|--------|------------|-------|---------|---------|
| 1   | IS318| Adams  | Database   | A     | Howser  | 60192   |
| 1   | IS301| Adams  | Program    | B     | Langley | 45869   |
| 2   | IS318| Jones  | Database   | A     | Howser  | 60192   |
| 3   | IS318| Smith  | Database   | B     | Howser  | 60192   |
| 4   | IS301| Baker  | Program    | A     | Langley | 45869   |
| 4   | IS318| Baker  | Database   | B     | Howser  | 60192   |

#### Normalized Tables:
1. **Students Table**:  
| SID | S_name |
|-----|--------|
| 1   | Adams  |
| 2   | Jones  |
| 3   | Smith  |
| 4   | Baker  |

2. **Courses Table**:  
| CID  | C_name   | Faculty  |
|------|----------|----------|
| IS318| Database | Howser   |
| IS301| Program  | Langley  |

3. **Faculty Table**:  
| Faculty | F_phone |
|---------|---------|
| Howser  | 60192   |
| Langley | 45869   |

4. **Enrollment Table**:  
| SID | CID   | Grade |
|-----|-------|-------|
| 1   | IS318 | A     |
| 1   | IS301 | B     |
| 2   | IS318 | A     |
| 3   | IS318 | B     |
| 4   | IS301 | A     |
| 4   | IS318 | B     |

---

### **Normalize to BCNF**

#### Input Table:
| OID  | O Date   | CID | C Name | C State | PID | P Desc  | P_Price | Qty |
|------|----------|-----|--------|---------|-----|---------|---------|-----|
| 1006 | 10/24/09 | 2   | Apex   | NC      | 7   | Table   | 800     | 1   |
| 1006 | 10/24/09 | 2   | Apex   | NC      | 5   | Desk    | 325     | 1   |
| 1006 | 10/24/09 | 2   | Apex   | NC      | 4   | Chair   | 200     | 5   |
| 1007 | 10/25/09 | 6   | Acme   | GA      | 11  | Dresser | 500     | 4   |
| 1007 | 10/25/09 | 6   | Acme   | GA      | 4   | Chair   | 200     | 6   |

#### Normalized Tables:
1. **Customer Table**:  
| CID | C_Name | C_State |
|-----|--------|---------|
| 2   | Apex   | NC      |
| 6   | Acme   | GA      |

2. **Product Table**:  
| PID | P Desc  | P_Price |
|-----|---------|---------|
| 7   | Table   | 800     |
| 5   | Desk    | 325     |
| 4   | Chair   | 200     |
| 11  | Dresser | 500     |

3. **Order Table**:  
| OID  | O Date   | CID |
|------|----------|-----|
| 1006 | 10/24/09 | 2   |
| 1007 | 10/25/09 | 6   |

4. **Order Details Table**:  
| OID  | PID | Qty |
|------|-----|-----|
| 1006 | 7   | 1   |
| 1006 | 5   | 1   |
| 1006 | 4   | 5   |
| 1007 | 11  | 4   |
| 1007 | 4   | 6   |

---

## **CheatSheet**

| **Normal Form** | **Condition**                                                              |
|------------------|---------------------------------------------------------------------------|
| **1NF**          | No multi-valued attributes                                               |
| **2NF**          | No partial dependencies (non-key attributes depend on part of the key)   |
| **3NF**          | No transitive dependencies                                               |
| **BCNF**         | Every functional dependency has a superkey on the left-hand side         |
| **4NF**          | No multi-valued dependencies                                             |
| **5NF**          | No join dependencies and decomposition is lossless                       |

---

✅ **Conclusion**:  
Normalization ensures efficient and logical database design by minimizing redundancy and avoiding anomalies in data operations.

---
