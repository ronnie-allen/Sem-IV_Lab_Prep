# Experiment 1: Configuring IAM in AWS

## 🌟 Aim
To explore AWS Identity and Access Management (IAM) by creating users, groups, and assigning permissions, and testing secure access to AWS services based on job roles.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **AWS IAM** | A secure way to control access to AWS services and resources by creating users, groups, and permissions. |
| **AWS Console** | Web-based interface for managing AWS services. |
| **IAM Policies** | Documents that define what actions are allowed or denied for users, groups, and roles. |
| **Incognito Mode** | A private browsing window used to test user logins without mixing sessions. |

---

## 🔥 Description
AWS Identity and Access Management (IAM) is critical for managing who can access what in the cloud.
In this experiment, three IAM users are created and assigned to different groups with different access permissions:
- **User-1** can only view S3 buckets.
- **User-2** can only view EC2 instances.
- **User-3** can start and stop EC2 instances.

Testing access ensures users cannot overstep their permissions.

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab** on your lab dashboard.
- Wait for the AWS link to turn **green**.
- Click on the AWS link to open the AWS Management Console.

### Step 2: Open IAM Service
- In the AWS Console, use the **search bar**.
- Type **IAM** and select it.

### Step 3: Explore IAM Users
- Click **Users** on the left sidebar.
- Review `user-1`, `user-2`, and `user-3`.
- Check their current **Permissions**, **Groups**, and **Security Credentials**.

### Step 4: Explore IAM Groups
- Click **User Groups**.
- Review `EC2-Admin`, `EC2-Support`, and `S3-Support` groups.
- See what **permissions** each group already has.

### Step 5: Review IAM Policies
- Expand the attached policies for groups:
  - `AmazonEC2ReadOnlyAccess` for EC2-Support
  - `AmazonS3ReadOnlyAccess` for S3-Support
  - `Inline policy` for EC2-Admin group (allows starting and stopping EC2 instances)

### Step 6: Assign Users to Groups
- Assign:
  - `user-1` → `S3-Support`
  - `user-2` → `EC2-Support`
  - `user-3` → `EC2-Admin`
- Confirm assignments are saved.

### Step 7: Verify Group Membership
- Check that each group has exactly **one user** assigned.

### Step 8: Test User Permissions
- Copy the **IAM sign-in URL**.
- Open a **private/incognito window**.

### Step 9: Test User-1
- Login as `user-1`.
- Check:
  - Access to S3 ✅
  - Denied access to EC2 ❌
- Logout.

### Step 10: Test User-2
- Login as `user-2`.
- Check:
  - Access to EC2 ✅
  - Denied access to S3 ❌
- Logout.

### Step 11: Test User-3
- Login as `user-3`.
- Start/Stop EC2 instances ✅
- Logout.

### Step 12: Submit the Lab
- Go back to the lab portal.
- Click **Submit**.

### Step 13: View the Submission Report
- Check your grading report.
- Correct errors if needed.

### Step 14: End the Lab
- Click **End Lab**.
- Close all AWS and lab tabs.

---

## 🎉 Conclusion
In this experiment, we successfully configured AWS IAM by creating and managing users, groups, and access permissions.
Testing confirmed that each user had only the specific access assigned to them.
This setup ensures secure cloud operations by implementing the principle of least privilege.

