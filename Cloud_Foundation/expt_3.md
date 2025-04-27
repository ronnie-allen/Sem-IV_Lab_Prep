# Experiment 3: Introduction to Amazon EC2

## 🌟 Aim
To understand how to launch, configure, manage, monitor, and resize an Amazon EC2 instance, and explore its security settings and cost-effective usage strategies.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **Amazon EC2 (Elastic Compute Cloud)** | A service that provides resizable compute capacity (virtual servers) in the cloud. |
| **Amazon Machine Image (AMI)** | A pre-configured image used to create virtual servers (EC2 instances). |
| **Security Groups** | Firewalls attached to EC2 instances that control traffic. |
| **Elastic Block Store (EBS)** | Persistent block storage for EC2 instances. |
| **CloudWatch** | Monitoring service to view system metrics like CPU utilization. |
| **Service Quotas** | AWS limits on resource usage, like number of EC2 instances per region. |

---

## 🔥 Description
Amazon EC2 allows users to rent virtual servers in the cloud to run applications. It supports flexible compute power, cost optimization, and the building of scalable cloud architectures.
In this experiment, we will:
- Launch an EC2 instance with basic configurations
- Host a sample web page
- Resize the instance to adjust compute resources
- Monitor the instance's health and performance
- Explore AWS quotas and stop protection features

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab** on your lab dashboard.
- Wait until the AWS link turns **green**.
- Open the AWS Management Console.

### Step 2: Launch Your EC2 Instance
- Go to the **EC2** service.
- Click **Launch Instance**.
- Configure:
  - Name: `Web Server`
  - AMI: `Amazon Linux 2023`
  - Instance Type: `t2.micro`
  - Key Pair: `vockey`
- Configure Networking:
  - VPC: `Lab VPC`
  - Subnet: `PublicSubnet1`
  - Enable auto-assign public IP
- Create a new **Security Group**:
  - Name: `Web Server Security Group`
  - Allow inbound HTTP traffic from Anywhere-IPv4
- Configure Storage:
  - Root Volume: 8 GiB EBS
- In **Advanced Details**, add this **User Data** script:
```bash
#!/bin/bash
dnf install -y httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```
- Launch the instance.
- Wait until **2/2 Status Checks** are passed.

### Step 3: Monitor the Instance
- Go to the **Status Checks** tab to verify instance health.
- Use **CloudWatch Monitoring** to view CPU, network, and disk activity.
- Under **Monitor and Troubleshoot**, access:
  - System logs
  - Instance screenshots (for troubleshooting)

### Step 4: Access the Web Server
- Copy the instance's **Public IPv4 address**.
- Paste it into your browser.
- You should see the message: `Hello From Your Web Server!`

If access fails:
- Check the **Security Group inbound rules**.
- Ensure HTTP (port 80) is allowed from Anywhere-IPv4.

### Step 5: Resize the Instance
- Stop the EC2 instance.
- Change instance type from `t2.micro` to `t2.small` (gives more RAM).
- Also, resize the attached EBS volume:
  - Change from 8 GiB to 10 GiB.
- Restart the instance.

### Step 6: Explore EC2 Limits
- Open **Service Quotas**.
- Search for **EC2**.
- Review resource limits, such as maximum On-Demand instances allowed per region.

### Step 7: Test Stop Protection
- Try to stop the instance.
- If stop protection is enabled, it will prevent you.
- Disable stop protection.
- Then stop the instance successfully.

### Step 8: Submit the Lab
- Return to your lab page.
- Click **Submit**.
- Wait for grading.

### Step 9: End the Lab
- Click **End Lab**.
- Close all AWS and lab tabs.

---

## 🎉 Conclusion
In this experiment, we launched and configured an EC2 instance, deployed a web server, resized the instance, monitored its performance, and explored AWS service quotas and stop protection.
This provided hands-on exposure to building and managing scalable cloud-based virtual machines inside AWS.
