# Experiment 5: Build Your DB Server and Interact with Your DB Using an App

## 🌟 Aim
To set up a MySQL database on Amazon RDS, configure security and networking, and connect it to a web application to perform database operations.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **Amazon RDS** | A managed relational database service that automates setup, scaling, and maintenance. |
| **Amazon VPC** | Private network environment to isolate and protect database resources. |
| **Security Groups** | Virtual firewalls that control inbound and outbound traffic to RDS and web servers. |
| **DB Subnet Group** | Defines which subnets Amazon RDS can use to deploy databases across multiple AZs. |
| **AWS Management Console** | Web interface for managing AWS services. |
| **Web Application** | A browser-accessible app used to connect to and interact with the database. |

---

## 🔥 Description
Amazon RDS simplifies setting up, operating, and scaling a relational database in the cloud.
In this experiment, we:
- Set up a secure, highly available MySQL database using Amazon RDS
- Configured networking with a DB subnet group
- Connected a web app to interact with the database (insert, edit, delete records)

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab**.
- Open AWS Management Console.

### Step 2: Create Security Group for RDS
- Go to **VPC** → **Security Groups**.
- Click **Create Security Group**:
  - Name: `DB Security Group`
  - Description: `Permit access from Web Security Group`
  - VPC: `Lab VPC`
- Add Inbound Rule:
  - Type: MySQL/Aurora (Port 3306)
  - Source: Web Security Group
- Click **Create**.

### Step 3: Create DB Subnet Group
- Go to **RDS** → **Subnet Groups**.
- Click **Create DB Subnet Group**:
  - Name: `DB-Subnet-Group`
  - VPC: `Lab VPC`
- Add subnets:
  - Availability Zones: `us-east-1a`, `us-east-1b`
  - Subnets CIDR: `10.0.1.0/24`, `10.0.3.0/24`

### Step 4: Create RDS Instance
- Go to **RDS** → **Databases** → **Create database**.
- Configure:
  - Engine: `MySQL`
  - Template: `Dev/Test`
  - Multi-AZ Deployment: Enabled
  - DB Identifier: `lab-db`
  - Master Username: `main`
  - Password: `lab-password`
- Instance settings:
  - DB Class: `db.t3.micro`
  - Storage: General Purpose (SSD), 20 GB
- Connectivity settings:
  - VPC: `Lab VPC`
  - Security Group: `DB Security Group`
- Disable Enhanced Monitoring.
- Initial DB name: `lab`
- Click **Create Database**.
- Wait for status to become **Available**.

### Step 5: Connect the Web App to RDS
- From AWS Details, copy the **WebServer IP address**.
- Open a new browser tab → Paste the IP address.
- In the web app, click **RDS** link.
- Enter database connection details:
  - Endpoint: RDS Endpoint (copied from RDS instance)
  - Database: `lab`
  - Username: `main`
  - Password: `lab-password`
- Click **Submit**.
- Test adding, editing, and deleting contacts.

### Step 6: Submit and End the Lab
- Click **Submit** on the lab portal.
- View submission results.
- Click **End Lab**.
- Close all browser tabs.

---

## 🎉 Conclusion
In this experiment, we successfully configured an Amazon RDS database, secured it with networking rules, and connected it to a web application to perform CRUD operations.
This exercise demonstrated real-world cloud database deployment and interaction through scalable and managed services.

