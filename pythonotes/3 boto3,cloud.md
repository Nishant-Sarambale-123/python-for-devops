🔥 Perfect Nishant!
Now we’re entering the **core level** — the most important part of **Python for Cloud & DevOps Automation**, where Python directly interacts with **AWS** and **Linux systems**.

Below are **very detailed notes (step-by-step)** with **clear DevOps use cases, examples, and explanations** — exactly how real-world automation scripts are written.

---

# 🚀 **3. Python for Cloud and DevOps Automation**

This section focuses on two key areas:

1. **AWS Cloud Automation (using boto3)**
2. **System & Server Automation (Linux, SSH, monitoring)**

---

## ☁️ **I. AWS Automation using Boto3**

### 🔹 What is Boto3?

* **Boto3** is the **AWS SDK for Python**.
* It allows Python scripts to **create, manage, and monitor** AWS services like EC2, S3, IAM, RDS, Lambda, CloudWatch, etc.

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

This saves credentials in:

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

# Create session (optional)
session = boto3.Session(profile_name="default")

# Create clients/resources
ec2 = boto3.client("ec2")
s3 = boto3.resource("s3")
```

✅ **DevOps Use Case:**
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
Generate an EC2 inventory report for all servers.

---

### **3️⃣ Start / Stop / Terminate Instances**

```python
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
Start/stop servers based on office hours to save AWS cost.

---

### **4️⃣ Create and Manage S3 Buckets**

```python
import boto3

s3 = boto3.resource("s3")

# List buckets
for bucket in s3.buckets.all():
    print(bucket.name)

# Create new bucket
bucket_name = "devops-nishant-demo"
s3.create_bucket(Bucket=bucket_name)
print("Bucket created")

# Delete bucket
s3.Bucket(bucket_name).delete()
```

✅ **Use Case:**
Automate backup bucket creation for logs and reports.

---

### **5️⃣ Upload / Download Files from S3**

```python
bucket = s3.Bucket("devops-nishant-demo")

# Upload
bucket.upload_file("backup.zip", "backup_2025.zip")
print("File uploaded")

# Download
bucket.download_file("backup_2025.zip", "restore.zip")
print("File downloaded")
```

✅ **Use Case:**
Push build artifacts or logs from Jenkins to S3 automatically.

---

### **6️⃣ Manage IAM Roles and Users**

```python
import boto3

iam = boto3.client("iam")

# List users
for user in iam.list_users()["Users"]:
    print(user["UserName"])

# Create a new IAM user
iam.create_user(UserName="devops-automation")
```

✅ **Use Case:**
Automate IAM user creation for temporary access or new developers.

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
Monitor DB health, create backups, or tag RDS resources.

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
Trigger Lambda for cleanup, event handling, or serverless deployments.

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
Fetch CPU utilization metrics for EC2 instances and generate performance reports.

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
print("Inventory report generated ✅")
```

✅ **Use Case:**
Keep track of all resources in your AWS environment for auditing or billing.

---

## 🖥️ **II. System and Server Automation (Linux + Python)**

Used for **daily admin tasks** like user management, log rotation, cron automation, and system monitoring.

---

### **1️⃣ Create Users, Groups, Permissions**

```python
import os

username = "appuser"

os.system(f"sudo useradd {username}")
os.system(f"sudo mkdir /home/{username}")
os.system(f"sudo chown {username}:{username} /home/{username}")
```

✅ **Use Case:**
Automatically create users for new deployments or servers.

---

### **2️⃣ Manage Cron Jobs**

```python
import os

# Add cron job
cron_command = 'echo "0 3 * * * /usr/bin/python3 /scripts/backup.py" >> /etc/crontab'
os.system(f"sudo bash -c '{cron_command}'")
```

✅ **Use Case:**
Automate nightly backups or log cleanups.

---

### **3️⃣ Disk Usage and Log Monitoring**

```python
import shutil

total, used, free = shutil.disk_usage("/")
print(f"Total: {total // (2**30)} GB")
print(f"Used: {used // (2**30)} GB")
print(f"Free: {free // (2**30)} GB")

if free / total < 0.1:
    print("⚠️ Low disk space!")
```

✅ **Use Case:**
Monitor disk space on EC2 servers and send alerts.

---

### **4️⃣ Using Paramiko for SSH Automation**

Install first:

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
Run commands on multiple EC2 servers remotely (update packages, deploy apps).

---

### **5️⃣ Using Subprocess to Run Shell Scripts**

```python
import subprocess

result = subprocess.run(["bash", "deploy.sh"], capture_output=True, text=True)
print(result.stdout)
```

✅ **Use Case:**
Integrate Python with existing shell scripts for CI/CD pipelines.

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
Monitor EC2 resource usage and send alerts to Slack or email.

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
    logging.warning("High CPU usage detected!")
```

✅ **Use Case:**
Health check script for server monitoring via cron.

---

## 📦 Summary Table

| Category              | Module             | Purpose                                  |
| --------------------- | ------------------ | ---------------------------------------- |
| **AWS Management**    | `boto3`            | EC2, S3, IAM, RDS, CloudWatch automation |
| **User Management**   | `os`               | Create users, change permissions         |
| **Cron Jobs**         | `os`               | Schedule automation tasks                |
| **Disk Monitoring**   | `shutil`, `psutil` | Check disk usage, free space             |
| **Remote SSH**        | `paramiko`         | Run commands on remote servers           |
| **Shell Integration** | `subprocess`       | Integrate Python & Bash                  |
| **Logging**           | `logging`          | Save system activity logs                |

---

## ✅ Real-World DevOps Automation Examples

| Task                    | Example                                                 |
| ----------------------- | ------------------------------------------------------- |
| Start/Stop EC2          | `boto3.ec2.start_instances()`                           |
| Upload backup to S3     | `boto3.s3.upload_file()`                                |
| Monitor disk usage      | `psutil.disk_usage()`                                   |
| Restart service via SSH | `paramiko.exec_command("sudo systemctl restart nginx")` |
| Automate cron job       | Add to `/etc/crontab` via Python                        |
| Generate cost report    | `boto3.cloudwatch.get_metric_data()`                    |
| Track EC2 uptime        | `datetime + psutil.boot_time()`                         |

---

Would you like me to create the next section —
**“4️⃣ Python CI/CD Automation” (Jenkins, GitHub Actions, Terraform, Docker)** —
in the same **step-by-step, DevOps-focused format**?
