Here is the **same content “AS IT IS”** but rewritten fully in **Python client syntax** (using `boto3.client()` everywhere).
No `resource()` used.
This matches **client-level SDK usage**, which is the standard for production & DevOps automation.

---

# 🚀 **3. Python for Cloud and DevOps Automation — CLIENT SYNTAX VERSION**

---

# ☁️ **I. AWS Automation using Boto3 — CLIENT SYNTAX**

---

## **1️⃣ Connect to AWS Account (Client Syntax)**

### **Initialize boto3 client**

```python
import boto3

s3_client = boto3.client("s3")
```

---

## **2️⃣ List EC2 Instances**

```python
import boto3

ec2 = boto3.client("ec2")

response = ec2.describe_instances()

for reservation in response["Reservations"]:
    for instance in reservation["Instances"]:
        print(f"ID: {instance['InstanceId']}, "
              f"State: {instance['State']['Name']}, "
              f"Type: {instance['InstanceType']}")
```

---

## **3️⃣ Start / Stop / Terminate Instances**

```python
import boto3

ec2 = boto3.client("ec2")
instance_id = "i-0abcd1234efgh5678"

# Start
ec2.start_instances(InstanceIds=[instance_id])
print("Instance started")

# Stop
ec2.stop_instances(InstanceIds=[instance_id])
print("Instance stopped")

# Terminate
ec2.terminate_instances(InstanceIds=[instance_id])
print("Instance terminated")
```

---

## **4️⃣ Create, List, Delete S3 Buckets (CLIENT)**

### **List buckets**

```python
import boto3

s3 = boto3.client("s3")

response = s3.list_buckets()

for bucket in response["Buckets"]:
    print(bucket["Name"])
```

### **Create bucket**

```python
s3.create_bucket(Bucket="devops-nishant-demo")
```

### **Delete bucket**

```python
s3.delete_bucket(Bucket="devops-nishant-demo")
```

---

## **5️⃣ Upload / Download Files from S3 (CLIENT)**

```python
import boto3

s3 = boto3.client("s3")
bucket = "devops-nishant-demo"

# Upload
s3.upload_file("backup.zip", bucket, "backup_2025.zip")
print("File uploaded")

# Download
s3.download_file(bucket, "backup_2025.zip", "restore.zip")
print("File downloaded")
```

---

## **6️⃣ IAM User Management (Client Syntax)**

```python
import boto3

iam = boto3.client("iam")

# List users
resp = iam.list_users()
for user in resp["Users"]:
    print(user["UserName"])

# Create user
iam.create_user(UserName="devops-automation")
```

---

## **7️⃣ RDS Client – Describe DBs**

```python
import boto3

rds = boto3.client("rds")

response = rds.describe_db_instances()

for db in response["DBInstances"]:
    print(f"DB Name: {db['DBInstanceIdentifier']}, "
          f"Status: {db['DBInstanceStatus']}")
```

---

## **8️⃣ Lambda Functions (List using client)**

```python
import boto3

lambda_client = boto3.client("lambda")

response = lambda_client.list_functions()

for fn in response["Functions"]:
    print(fn["FunctionName"])
```

---

## **9️⃣ CloudWatch Metrics (Client)**

```python
import boto3

cloudwatch = boto3.client("cloudwatch")

metrics = cloudwatch.list_metrics(
    Namespace="AWS/EC2",
    MetricName="CPUUtilization"
)

for m in metrics["Metrics"]:
    print(m)
```

---

## **🔟 Generate AWS EC2 Inventory CSV (Client)**

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

print("Inventory report generated ✔️")
```

---

# 🖥️ **II. System & Server Automation (Linux + Python)**

*(Client syntax not needed here — normal Python modules)*

---

## **1️⃣ Create Users, Groups, Permissions**

```python
import os

username = "appuser"

os.system(f"sudo useradd {username}")
os.system(f"sudo mkdir /home/{username}")
os.system(f"sudo chown {username}:{username} /home/{username}")
```

---

## **2️⃣ Manage Cron Jobs**

```python
import os

cron = 'echo "0 3 * * * /usr/bin/python3 /scripts/backup.py" >> /etc/crontab'
os.system(f"sudo bash -c '{cron}'")
```

---

## **3️⃣ Disk Usage**

```python
import shutil

total, used, free = shutil.disk_usage("/")

print(f"Total: {total//(2**30)} GB")
print(f"Used: {used//(2**30)} GB")
print(f"Free: {free//(2**30)} GB")
```

---

## **4️⃣ SSH Automation using Paramiko**

```python
import paramiko

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

ssh.connect(
    hostname="192.168.1.10",
    username="ec2-user",
    key_filename="awskey.pem"
)

stdin, stdout, stderr = ssh.exec_command("uptime")
print(stdout.read().decode())

ssh.close()
```

---

## **5️⃣ Run Bash Scripts via Python**

```python
import subprocess

result = subprocess.run(["bash", "deploy.sh"], capture_output=True, text=True)
print(result.stdout)
```

---

## **6️⃣ System Monitoring using psutil**

```python
import psutil

print("CPU:", psutil.cpu_percent())
print("Memory:", psutil.virtual_memory().percent)
print("Disk:", psutil.disk_usage('/').percent)
```

---

## **7️⃣ Logging + Monitoring**

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

---

# 🔥 NEXT SECTION READY

I can generate **“4️⃣ Python CI/CD Automation (Jenkins + GitHub Actions + Terraform + Docker)”** also in **client syntax & DevOps format**.

Would you like it?
