# ☁️ Cloud Foundations Lab - Cheat Sheet

---

## Experiment 1: Configuring IAM in AWS

🔹 Create 3 users: user-1, user-2, user-3  
🔹 Create groups: EC2-Admin, EC2-Support, S3-Support  
🔹 Assign users to groups:
- user-1 → S3-Support
- user-2 → EC2-Support
- user-3 → EC2-Admin

🔹 Test each user’s access:
- user-1 → S3 only ✅
- user-2 → EC2 only ✅
- user-3 → Start/Stop EC2 ✅

---

## Experiment 2: Building a VPC and Launching a Web Server

🔹 Create VPC: `10.0.0.0/16`  
🔹 Create 2 Public Subnets and 2 Private Subnets  
🔹 Create Internet Gateway (for public access) and NAT Gateway (for private internet access)  
🔹 Configure Route Tables:
- Public subnets use IGW
- Private subnets use NAT

🔹 Create Security Group for HTTP  
🔹 Launch EC2 (`t2.micro`, Amazon Linux) in public subnet  
🔹 User Data script installs Apache and deploys web app  
🔹 Access website using Public DNS.

---

## Experiment 3: Introduction to Amazon EC2

🔹 Launch EC2 instance:
- AMI: Amazon Linux 2023
- Type: t2.micro
- User Data to install Apache and host a sample page

🔹 Monitor instance health (Status Checks, CloudWatch)

🔹 Resize instance:
- Change to t2.small
- Expand EBS volume from 8 GB to 10 GB

🔹 Test stop protection  
🔹 Explore EC2 Service Quotas

---

## Experiment 4: Working with Amazon EBS

🔹 Create EBS volume (1 GiB)  
🔹 Attach volume to EC2 (device `/dev/sdf`)  
🔹 Format and mount:
```bash
sudo mkfs -t ext3 /dev/sdf
sudo mkdir /mnt/data-store
sudo mount /dev/sdf /mnt/data-store
```
🔹 Create a file inside mounted volume  
🔹 Create Snapshot of EBS volume  
🔹 Delete file and restore volume from snapshot  
🔹 Attach restored volume and recover data

---

## Experiment 5: Build Your DB Server and Interact with Your DB Using an App

🔹 Create Security Group for RDS (allow MySQL port 3306)  
🔹 Create DB Subnet Group across 2 AZs  
🔹 Launch RDS Instance:
- Engine: MySQL
- Multi-AZ Enabled
- Username: `main`
- Password: `lab-password`

🔹 Connect web app to RDS endpoint  
🔹 Perform CRUD operations (add, edit, delete contacts)

---

## Experiment 6: Configure Load Balancer and Auto Scaling

🔹 Create AMI from Web Server 1  
🔹 Create Target Group: `LabGroup`  
🔹 Create Application Load Balancer (ALB): `LabELB`  
🔹 Create Launch Template using AMI  
🔹 Create Auto Scaling Group:
- Min: 2 instances
- Max: 6 instances
- Target CPU: 60%

🔹 Perform Load Test to trigger scaling  
🔹 Verify additional instances created automatically  
🔹 Terminate Web Server 1 to test fault tolerance (ELB keeps app running)

---

# 🚀 Quick AWS Commands/Scripts

- **Format and Mount EBS**:
```bash
sudo mkfs -t ext3 /dev/sdf
sudo mkdir /mnt/data-store
sudo mount /dev/sdf /mnt/data-store
```
- **Add to fstab**:
```bash
echo "/dev/sdf /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```
- **Basic Apache Setup (User Data script)**:
```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

---

# 🎯 Important Points to Remember
- Always **Enable Auto-assign Public IP** for EC2 web servers.
- Always **Create correct Security Group rules** (HTTP, MySQL, etc.)
- Always **Use correct VPC/Subnet** settings.
- Wait for **2/2 status checks** before accessing an EC2 or RDS instance.
- Keep track of **region** (mostly N. Virginia - us-east-1).

---

✅ That's your **complete cheat sheet** for Cloud Foundations Laboratory!
