# Experiment 4: Working with Amazon EBS

## 🌟 Aim
To understand how to create, attach, format, and restore an Amazon Elastic Block Store (EBS) volume for an EC2 instance, including creating snapshots for backup and recovery.

---

## 📚 Tools Used

| Tool | Definition |
|-----|------------|
| **Amazon EBS** | Elastic Block Store - durable, block-level storage for EC2 instances. |
| **EC2 Instance** | A virtual server to which EBS volumes are attached. |
| **Snapshot** | A backup copy of an EBS volume at a specific point in time. |
| **AWS Management Console** | Web-based portal to manage AWS services. |
| **Linux Shell** | Command-line interface to manage EC2 and EBS resources. |

---

## 🔥 Description
Amazon EBS provides scalable, persistent storage for EC2 instances. In this experiment, we will:
- Create and attach an EBS volume to an EC2 instance.
- Format and mount the volume for use.
- Create a snapshot for backup.
- Delete data and recover it by restoring from a snapshot.

---

## 🛠️ Step-by-Step Procedure

### Step 1: Start the Lab
- Click **Start Lab**.
- Open the AWS Console.

### Step 2: Create and Attach an EBS Volume
- Navigate to **EC2** > **Volumes**.
- Click **Create Volume**:
  - Type: `gp2`
  - Size: `1 GiB`
  - AZ: Same as the Lab EC2 instance (e.g., `us-east-1a`).
- Tag it: `Name = My Volume`.
- After creation, select the volume and click **Actions → Attach Volume**.
- Attach to the `Lab` instance at device `/dev/sdf`.

### Step 3: Connect to EC2 Instance
- Open **EC2 Instances**.
- Click **Connect** → Use **EC2 Instance Connect**.
- Open the Linux shell.

### Step 4: Format and Mount the Volume
- Run to format:
```bash
sudo mkfs -t ext3 /dev/sdf
```
- Create mount directory:
```bash
sudo mkdir /mnt/data-store
```
- Mount the volume:
```bash
sudo mount /dev/sdf /mnt/data-store
```
- Make it auto-mount after reboot:
```bash
echo "/dev/sdf /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### Step 5: Create a File
- Create and write a file:
```bash
sudo sh -c "echo 'This is a test file' > /mnt/data-store/file.txt"
```
- Verify the file:
```bash
cat /mnt/data-store/file.txt
```

### Step 6: Create a Snapshot
- Go to **Volumes**.
- Select `My Volume` → **Actions → Create Snapshot**.
- Tag: `Name = My Snapshot`.

### Step 7: Delete and Restore the File
- Delete the file:
```bash
sudo rm /mnt/data-store/file.txt
```
- Verify deletion:
```bash
ls /mnt/data-store/
```
- Go to **Snapshots** → Select `My Snapshot` → **Create Volume**.
- Attach new volume (`Restored Volume`) to the Lab instance at `/dev/sdg`.

### Step 8: Mount and Verify Restored Volume
- Create a new mount directory:
```bash
sudo mkdir /mnt/data-store2
```
- Mount restored volume:
```bash
sudo mount /dev/sdg /mnt/data-store2
```
- Verify recovered file:
```bash
ls /mnt/data-store2/
```

### Step 9: Submit and End Lab
- Click **Submit** in the lab portal.
- End Lab and close all tabs.

---

## 🎉 Conclusion
We successfully demonstrated the creation, usage, backup, and restoration of an Amazon EBS volume attached to an EC2 instance.
This ensures data persistence, recovery from failures, and practical understanding of AWS storage services.

