Absolutely 🔥 Nishant!
Here’s your **Python for Cloud & DevOps Automation (Part 3)** — fully **formatted**, **clean**, and **ready-to-use** as a **professional study or documentation reference**.

It includes your **updated S3 Client version**, consistent styling, and DevOps-focused layout 👇

---

# 🚀 **3. Python for Cloud and DevOps Automation**

This section focuses on two key areas:

1. **AWS Cloud Automation (using boto3)**
2. **System & Server Automation (Linux, SSH, Monitoring)**

---

## ☁️ **I. AWS Automation using Boto3**

### 🔹 What is Boto3?

* **Boto3** is the **AWS SDK for Python**.
* It allows Python scripts to **create, manage, and monitor** AWS services like **EC2, S3, IAM, RDS, Lambda, CloudWatch**, etc.

---

### **1️⃣ Connect to AWS Account**

#### **Step 1:** Install boto3

```bash
pip install boto3
```

#### **Step 2:** Configure AWS credentials

```bash
aws configure
```

This stores credentials in:

```
~/.aws/credentials
[default]
aws_access_key_id = <your_access_key>
aws_secret_access_key = <your_secret_key>
region = ap-south-1
```

#### **Step 3:** Initialize boto3

```python
import boto3

# Create S3 client
s3_client = boto3.client('s3')

bucket_name = "devops-nishant-demo"

# ---------- Upload file ----------
s3_client.upload_file("backup.zip", bucket_name, "backup_2025.zip")
print("✅ File uploaded successfully to S3")

# ---------- Download file ----------
s3_client.download_file(bucket_name, "backup_2025.zip", "restore.zip")
print("✅ File downloaded successfully from S3")
```

✅ **Use Case:**
Connect to AWS and use the same credentials for automation scripts and CI/CD pipelines.

---

### **2️⃣ List EC2 Instances**

```python
import boto3

ec2 = boto3.client("ec2")

response = ec2.describe_instances()

for reservation in response["Reservations"]:
    for instance in reservation["Instances"]:
        print(f"ID: {instance['InstanceId']}, State: {instance['State']['Name']}, Type: {instance['InstanceType']}")
```

✅ **Use Case:**
Generate an EC2 inventory report for all running servers.

---

### **3️⃣ Start / Stop / Terminate Instances**

```python
import boto3

ec2 = boto3.client("ec2")
instance_id = "i-0abcd1234efgh5678"

# Start instance
ec2.start_instances(InstanceIds=[instance_id])
print("Instance started")

# Stop instance
ec2.stop_instances(InstanceIds=[instance_id])
print("Instance stopped")

# Terminate instance
ec2.terminate_instances(InstanceIds=[instance_id])
print("Instance terminated")
```

✅ **Use Case:**
Start or stop servers based on office hours to save AWS costs.

---

### **4️⃣ Create and Manage S3 Buckets (Client Version)**

```python
import boto3

# Create an S3 client
s3_client = boto3.client("s3")

# ---------- List all buckets ----------
response = s3_client.list_buckets()
print("Available Buckets:")
for bucket in response["Buckets"]:
    print(f"- {bucket['Name']}")

# ---------- Create a new bucket ----------
bucket_name = "devops-nishant-demo"
s3_client.create_bucket(
    Bucket=bucket_name,
    CreateBucketConfiguration={'LocationConstraint': 'ap-south-1'}
)
print(f"✅ Bucket '{bucket_name}' created successfully.")

# ---------- Delete the bucket ----------
s3_client.delete_bucket(Bucket=bucket_name)
print(f"🗑️ Bucket '{bucket_name}' deleted successfully.")
```

✅ **Use Case:**
Automate bucket lifecycle management — creating, listing, and deleting buckets for build artifacts or log storage.

---

### **5️⃣ Upload / Download Files from S3**

```python
import boto3

s3_client = boto3.client("s3")
bucket_name = "devops-nishant-demo"

# Upload
s3_client.upload_file("backup.zip", bucket_name, "backup_2025.zip")
print("File uploaded successfully ✅")

# Download
s3_client.download_file(bucket_name, "backup_2025.zip", "restore.zip")
print("File downloaded successfully ✅")
```

✅ **Use Case:**
Push build artifacts or logs from Jenkins pipelines to S3 automatically.

---

### **6️⃣ Manage IAM Users and Roles**

```python
import boto3

iam = boto3.client("iam")

# List users
for user in iam.list_users()["Users"]:
    print(user["UserName"])

# Create a new IAM user
iam.create_user(UserName="devops-automation")
print("✅ IAM user created successfully.")
```

✅ **Use Case:**
Automate IAM user creation for new developers or temporary access.

---

### **7️⃣ Work with RDS (Databases)**

```python
import boto3

rds = boto3.client("rds")

# List all RDS instances
response = rds.describe_db_instances()
for db in response["DBInstances"]:
    print(f"DB Name: {db['DBInstanceIdentifier']}, Status: {db['DBInstanceStatus']}")
```

✅ **Use Case:**
Monitor RDS health and automate snapshot creation or tagging.

---

### **8️⃣ AWS Lambda Functions**

```python
import boto3

lambda_client = boto3.client("lambda")

response = lambda_client.list_functions()
for fn in response["Functions"]:
    print(f"Lambda: {fn['FunctionName']}")
```

✅ **Use Case:**
Trigger Lambda for cleanup tasks or event-based automation.

---

### **9️⃣ CloudWatch Monitoring**

```python
import boto3

cloudwatch = boto3.client("cloudwatch")

metrics = cloudwatch.list_metrics(Namespace="AWS/EC2", MetricName="CPUUtilization")
for m in metrics["Metrics"]:
    print(m)
```

✅ **Use Case:**
Fetch EC2 performance metrics for monitoring and alerting.

---

### **🔟 Generate AWS Resource Inventory**

```python
import boto3
import csv

ec2 = boto3.client("ec2")
instances = ec2.describe_instances()

with open("aws_inventory.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["InstanceID", "Type", "State", "PrivateIP"])

    for reservation in instances["Reservations"]:
        for instance in reservation["Instances"]:
            writer.writerow([
                instance["InstanceId"],
                instance["InstanceType"],
                instance["State"]["Name"],
                instance.get("PrivateIpAddress", "N/A")
            ])

print("✅ AWS inventory report generated successfully!")
```

✅ **Use Case:**
Generate AWS instance inventory for auditing or billing.

---

## 🖥️ **II. System and Server Automation (Linux + Python)**

Used for **daily admin tasks**, **system monitoring**, and **DevOps automation**.

---

### **1️⃣ Create Users, Groups, Permissions**

```python
import os

username = "appuser"

os.system(f"sudo useradd {username}")
os.system(f"sudo mkdir /home/{username}")
os.system(f"sudo chown {username}:{username} /home/{username}")
print(f"✅ User '{username}' created successfully.")
```

✅ **Use Case:**
Automatically create system users for new application deployments.

---

### **2️⃣ Manage Cron Jobs**

```python
import os

# Add cron job
cron_command = 'echo "0 3 * * * /usr/bin/python3 /scripts/backup.py" >> /etc/crontab'
os.system(f"sudo bash -c '{cron_command}'")
print("✅ Cron job added successfully.")
```

✅ **Use Case:**
Automate scheduled backups or cleanup tasks.

---

### **3️⃣ Disk Usage and Log Monitoring**

```python
import shutil

total, used, free = shutil.disk_usage("/")
print(f"Total: {total // (2**30)} GB")
print(f"Used: {used // (2**30)} GB")
print(f"Free: {free // (2**30)} GB")

if free / total < 0.1:
    print("⚠️ Warning: Low disk space!")
```

✅ **Use Case:**
Monitor disk space on servers and trigger alerts.

---

### **4️⃣ Using Paramiko for SSH Automation**

Install Paramiko first:

```bash
pip install paramiko
```

Code:

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

ssh.connect(hostname="192.168.1.10", username="ec2-user", key_filename="awskey.pem")

stdin, stdout, stderr = ssh.exec_command("uptime")
print(stdout.read().decode())

ssh.close()
```

✅ **Use Case:**
Remotely execute Linux commands on EC2 instances (deployments, restarts, updates).

---

### **5️⃣ Using Subprocess to Run Shell Scripts**

```python
import subprocess

result = subprocess.run(["bash", "deploy.sh"], capture_output=True, text=True)
print(result.stdout)
```

✅ **Use Case:**
Integrate Python with existing Bash or shell scripts in CI/CD workflows.

---

### **6️⃣ Using psutil for System Monitoring**

Install:

```bash
pip install psutil
```

Code:

```python
import psutil

print(f"CPU Usage: {psutil.cpu_percent()}%")
print(f"Memory Usage: {psutil.virtual_memory().percent}%")
print(f"Disk Usage: {psutil.disk_usage('/').percent}%")
```

✅ **Use Case:**
Monitor system performance and resource utilization.

---

### **7️⃣ Combine Monitoring + Logging Example**

```python
import psutil, logging
from datetime import datetime

logging.basicConfig(filename="system_health.log", level=logging.INFO)

cpu = psutil.cpu_percent()
mem = psutil.virtual_memory().percent

logging.info(f"{datetime.now()} - CPU: {cpu}%, MEM: {mem}%")

if cpu > 80:
    logging.warning("⚠️ High CPU usage detected!")
```

✅ **Use Case:**
Implement system health logging and integrate with alerts or monitoring tools.

---

## 📦 **Summary Table**

| Category              | Module             | Purpose                                  |
| --------------------- | ------------------ | ---------------------------------------- |
| **AWS Management**    | `boto3`            | EC2, S3, IAM, RDS, CloudWatch automation |
| **User Management**   | `os`               | Create users, modify permissions         |
| **Cron Jobs**         | `os`               | Schedule tasks automatically             |
| **Disk Monitoring**   | `shutil`, `psutil` | Monitor disk space and system health     |
| **Remote SSH**        | `paramiko`         | Execute remote commands on servers       |
| **Shell Integration** | `subprocess`       | Run shell scripts from Python            |
| **Logging**           | `logging`          | Record system events and warnings        |

---

## ✅ **Real-World DevOps Automation Examples**

| Task                    | Example                                                 |
| ----------------------- | ------------------------------------------------------- |
| Start/Stop EC2          | `boto3.ec2.start_instances()`                           |
| Upload backup to S3     | `boto3.s3.upload_file()`                                |
| Monitor disk usage      | `psutil.disk_usage()`                                   |
| Restart service via SSH | `paramiko.exec_command("sudo systemctl restart nginx")` |
| Automate cron job       | Add job to `/etc/crontab` via Python                    |
| Generate cost report    | `boto3.cloudwatch.get_metric_data()`                    |
| Track EC2 uptime        | `datetime + psutil.boot_time()`                         |

---

🔥 **Next Module → “4️⃣ Python CI/CD Automation”**
Would you like me to continue with that next — covering **Jenkins, GitHub Actions, Terraform, and Docker automation** — in the same detailed DevOps format?
