# Experiment 2: Building a VPC and Launching a Web Server

## 🌟 Aim
To create a Virtual Private Cloud (VPC) in AWS, configure its network components, set up a security group, and launch an EC2 instance running a web server inside the VPC.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **AWS VPC** | Virtual Private Cloud - your private network in AWS where you can define IP address ranges, subnets, and routing rules. |
| **Subnet** | A small section of a VPC to organize resources (like public and private areas). |
| **Internet Gateway** | A gateway to allow public internet access into your VPC. |
| **NAT Gateway** | Allows private subnets to access the internet without being directly exposed. |
| **Route Tables** | Routing instructions that define how traffic moves inside the VPC. |
| **Security Groups** | Firewalls that control incoming and outgoing traffic to AWS resources. |
| **EC2 Instance** | A virtual machine (server) running inside AWS. |

---

## 🔥 Description
Amazon Virtual Private Cloud (VPC) allows you to launch AWS resources into a logically isolated network that you define.
In this experiment, we will:
- Build a custom VPC
- Create public and private subnets
- Configure internet access
- Set up a security group
- Launch a web server inside the public subnet

This structure mirrors how real-world cloud environments are built.

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab** on your lab dashboard.
- Wait for the AWS link to turn **green**.
- Open the AWS Management Console.

### Step 2: Create a VPC
- Go to the **VPC** service.
- Click **Create VPC** → Choose **VPC and more**.
- Configure:
  - Name: `lab-vpc`
  - IPv4 CIDR Block: `10.0.0.0/16`
  - 1 Public Subnet: `10.0.0.0/24`
  - 1 Private Subnet: `10.0.1.0/24`
  - Availability Zone: `us-east-1a`
  - Enable DNS Hostnames and DNS Resolution.
- Under NAT Gateway options, create a NAT Gateway in the public subnet.
- Click **Create VPC**.

### Step 3: Create Additional Subnets
- In the VPC Dashboard, go to **Subnets**.
- Click **Create Subnet**:
  - Subnet Name: `lab-subnet-public2`
  - AZ: `us-east-1b`
  - CIDR: `10.0.2.0/24`
- Create another subnet:
  - Subnet Name: `lab-subnet-private2`
  - AZ: `us-east-1b`
  - CIDR: `10.0.3.0/24`

### Step 4: Configure Route Tables
- Go to **Route Tables**.
- Select `lab-rtb-private1-us-east-1a` → Edit Subnet Associations → Add `lab-subnet-private2`.
- Select `lab-rtb-public` → Edit Subnet Associations → Add `lab-subnet-public2`.

### Step 5: Create a Security Group
- Navigate to **Security Groups**.
- Click **Create Security Group**:
  - Name: `Web Security Group`
  - Description: Enable HTTP access
  - VPC: `lab-vpc`
- Under Inbound Rules, add:
  - Type: HTTP
  - Source: Anywhere-IPv4
- Save the security group.

### Step 6: Launch a Web Server Instance
- Go to **EC2** → Click **Launch Instance**.
- Configure:
  - Name: `Web Server 1`
  - AMI: `Amazon Linux 2023`
  - Instance Type: `t2.micro`
  - Key Pair: `vockey`
  - Network: `lab-vpc`
  - Subnet: `lab-subnet-public2`
  - Auto-assign Public IP: Enabled
  - Security Group: `Web Security Group`
- Scroll to **Advanced Details** and paste the following in **User Data**:
```bash
#!/bin/bash
# Install Apache Web Server and PHP
dnf install -y httpd wget php mariadb105-server
# Download and set up the lab web app
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
# Enable and start Apache service
chkconfig httpd on
service httpd start
```
- Click **Launch Instance**.
- Wait until **2/2 Status Checks** are passed.

### Step 7: Test the Web Server
- Go to **EC2** → Select `Web Server 1`.
- Copy the **Public IPv4 DNS**.
- Open a new browser tab and paste the DNS.
- Verify that you see a web page with the AWS logo and instance metadata.

### Step 8: Submit the Lab
- Return to your lab portal.
- Click **Submit** and wait for grading.

### Step 9: End the Lab
- Click **End Lab**.
- Close all AWS and lab-related tabs.

---

## 🎉 Conclusion
In this experiment, we successfully built a custom VPC with public and private subnets, configured routing and security, and deployed a web server accessible over the internet.
This setup mirrors real-world cloud networking practices, enabling scalable and secure deployments inside AWS.

