# Ex-10: Normalization and Denormalization

## Objective
The objective of this exercise is to normalize the tables for a given application and understand the process of denormalization.

---

## What is Normalization?
Normalization is a process in database design that organizes tables to reduce redundancy and improve data integrity. By applying a series of rules, known as **normal forms**, it ensures an optimal and logical design.

### Types of Normal Forms
| **Normal Form** | **Condition**                                                                  |
|------------------|-------------------------------------------------------------------------------|
| **1NF**          | All attributes must contain atomic values.                                   |
| **2NF**          | Must be in 1NF, and all non-key attributes must depend on the entire primary key. |
| **3NF**          | Must be in 2NF, and there should be no transitive dependencies.              |
| **BCNF**         | Must be in 3NF, and all functional dependencies must have a superkey.        |
| **4NF**          | No multi-valued dependencies.                                               |
| **5NF**          | Cannot be decomposed further without losing data (lossless decomposition).  |

---

## Example Normalization Process

### 1. First Normal Form (1NF)
#### Input Table:
| Instructor Name | Course Code       |
|-----------------|-------------------|
| Prof. George    | CS101, CS154      |
| Prof. Atkins    | CS152             |

#### Normalized Table:
| Instructor Name | Course Code |
|-----------------|-------------|
| Prof. George    | CS101       |
| Prof. George    | CS154       |
| Prof. Atkins    | CS152       |

---

### 2. Second Normal Form (2NF)
#### Input Table:
| Student Name | Course Code |
|--------------|-------------|
| Rahul        | CS152       |
| Rajat        | CS101       |
| Rahul        | CS154       |
| Raman        | CS101       |

#### Normalized Tables:
**Students Table:**
| Student Name | Enrolment Number |
|--------------|------------------|
| Rahul        | 1                |
| Rajat        | 2                |
| Raman        | 3                |

**Courses Table:**
| Course Code | Enrolment Number |
|-------------|------------------|
| CS152       | 1                |
| CS154       | 1                |
| CS101       | 2                |
| CS101       | 3                |

---

### 3. Third Normal Form (3NF)
#### Input Table:
| Course Code | Venue           | Instructor Name | Department             |
|-------------|-----------------|-----------------|------------------------|
| MA214       | Lecture Hall 18 | Prof. Ronald    | Mathematics Department |
| ME112       | Auditorium      | Prof. John      | Electronics Department |

#### Normalized Tables:
**Courses Table:**
| Course Code | Venue           | Instructor ID |
|-------------|-----------------|---------------|
| MA214       | Lecture Hall 18 | 1             |
| ME112       | Auditorium      | 2             |

**Instructors Table:**
| Instructor ID | Instructor Name | Department             |
|---------------|-----------------|------------------------|
| 1             | Prof. Ronald    | Mathematics Department |
| 2             | Prof. John      | Electronics Department |

---

### 4. Boyce-Codd Normal Form (BCNF)
#### Input Table:
| OID  | Order Date | CID | Customer Name | Customer State | PID | Product Description | Product Price | Quantity |
|------|------------|-----|---------------|----------------|-----|----------------------|---------------|----------|
| 1006 | 10/24/09   | 2   | Apex          | NC             | 7   | Table               | 800           | 1        |
| 1006 | 10/24/09   | 2   | Apex          | NC             | 5   | Desk                | 325           | 1        |

#### Normalized Tables:
**Customer Table:**
| CID | Customer Name | Customer State |
|-----|---------------|----------------|
| 2   | Apex          | NC             |

**Product Table:**
| PID | Product Description | Product Price |
|-----|----------------------|---------------|
| 7   | Table               | 800           |
| 5   | Desk                | 325           |

**Order Table:**
| OID  | Order Date | CID |
|------|------------|-----|
| 1006 | 10/24/09   | 2   |

**Order Details Table:**
| OID  | PID | Quantity |
|------|-----|----------|
| 1006 | 7   | 1        |
| 1006 | 5   | 1        |

---

## Denormalization
Denormalization involves combining tables to optimize database performance at the cost of redundancy. For example:
- Joining **Customers** and **Orders** tables to reduce query complexity.

---

## CheatSheet for Normal Forms
| **Normal Form** | **Condition**                                                                  |
|------------------|-------------------------------------------------------------------------------|
| **1NF**          | Attributes must have atomic values.                                          |
| **2NF**          | All non-key attributes must depend on the entire primary key.               |
| **3NF**          | No transitive dependencies.                                                 |
| **BCNF**         | Every functional dependency must have a superkey.                           |
| **4NF**          | No multi-valued dependencies.                                               |
| **5NF**          | Ensures no loss of data during decomposition.                               |

---

## Results
The database tables were successfully normalized, reducing redundancy and improving the structure for efficient operations.

---
Made with 🫶🏻 by Franz Kingstein


