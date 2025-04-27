# Experiment 6: Configure Load Balancer and Auto Scaling in AWS

## 🌟 Aim
To set up an Elastic Load Balancer (ELB) and an Auto Scaling Group (ASG) in AWS for distributing incoming traffic and automatically scaling EC2 instances based on demand.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **Elastic Load Balancer (ELB)** | Distributes incoming application traffic across multiple EC2 instances to increase availability. |
| **Auto Scaling Group (ASG)** | Automatically adjusts the number of EC2 instances based on system load. |
| **Amazon Machine Image (AMI)** | A snapshot of an EC2 instance configuration used to launch new instances. |
| **Launch Template** | A configuration template used by Auto Scaling groups to launch EC2 instances. |
| **Amazon CloudWatch** | Monitors AWS resources and triggers alarms for scaling actions. |
| **AWS Management Console** | Web portal for managing AWS services. |

---

## 🔥 Description
This experiment focuses on building a fault-tolerant system that automatically handles high or low traffic loads by distributing traffic across multiple servers and scaling the number of instances up or down as needed.
We achieve this by creating a load balancer and an auto-scaling setup linked with monitoring alarms.

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab**.
- Open the AWS Console.

### Step 2: Create an AMI from Web Server 1
- Go to **EC2** > **Instances**.
- Select `Web Server 1`.
- Click **Actions → Image and templates → Create image**.
- Name: `WebServerAMI`.
- Click **Create Image**.

### Step 3: Create Target Group and Load Balancer
- Go to **EC2** > **Target Groups**.
- Click **Create Target Group**:
  - Type: `Instances`
  - Name: `LabGroup`
  - VPC: `Lab VPC`
- Then, go to **Load Balancers** > **Create Load Balancer**:
  - Type: `Application Load Balancer`
  - Name: `LabELB`
  - Scheme: `Internet-facing`
  - Select public subnets
  - Assign `Web Security Group`
  - Listener: Forward to `LabGroup`
- Click **Create Load Balancer**.

### Step 4: Create Launch Template and Auto Scaling Group
- Go to **Launch Templates**.
- Click **Create Launch Template**:
  - Name: `LabConfig`
  - AMI: `WebServerAMI`
  - Instance Type: `t2.micro`
  - Key Pair: `vockey`
  - Security Group: `Web Security Group`
- After creation, click **Create Auto Scaling Group**:
  - Name: `Lab Auto Scaling Group`
  - Launch Template: `LabConfig`
  - VPC: `Lab VPC`
  - Subnets: Private Subnets
  - Attach to Load Balancer: `LabGroup`
  - Scaling Policy:
    - Target 60% CPU utilization
    - Minimum: 2 instances
    - Maximum: 6 instances
- Click **Create Auto Scaling Group**.

### Step 5: Test Load Balancer
- Go to **Load Balancers** > Select `LabELB`.
- Copy the **DNS name**.
- Open a browser tab and paste it.
- Verify that the web page loads.

### Step 6: Test Auto Scaling
- Open **CloudWatch** > **Alarms**.
- Confirm the existence of:
  - `AlarmHigh` (scale out)
  - `AlarmLow` (scale in)
- Go back to the web app and perform **Load Test**.
- Wait for Auto Scaling to launch new instances based on CPU load.

### Step 7: Terminate Web Server 1
- Go to **EC2 Instances**.
- Select `Web Server 1`.
- Click **Instance State → Terminate**.
- Confirm termination.
- Web application remains accessible through ELB.

### Step 8: Submit and End the Lab
- Click **Submit**.
- Wait for grading.
- End the Lab.

---

## 🎉 Conclusion
This experiment demonstrated setting up a load-balanced and auto-scaled architecture using Amazon EC2, Elastic Load Balancer, Auto Scaling Groups, and CloudWatch alarms.
The system automatically handled traffic spikes and failures, ensuring high availability and scalability with minimal manual intervention.

