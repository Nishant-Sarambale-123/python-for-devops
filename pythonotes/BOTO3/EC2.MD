Sure! Let's make **detailed notes on EC2 instance operations using Boto3** for DevOps purposes, and then I’ll give you a **practical exam-style question with answers**. I’ll break it down clearly so it’s easy to revise.

---

## **EC2 Instance Operations Using Boto3 (Python)**

### **1. Setup**

Before using Boto3, ensure:

* AWS credentials (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`) are configured via `~/.aws/credentials` or environment variables.
* Boto3 is installed:

```bash
pip install boto3
```

Import Boto3 and create a client or resource:

```python
import boto3

# Using client
ec2_client = boto3.client('ec2', region_name='us-east-1')

# Using resource
ec2_resource = boto3.resource('ec2', region_name='us-east-1')
```

> **Tip:** `resource` is higher-level, easier for object-oriented operations. `client` is lower-level, more API-like.

---

### **2. Launch an EC2 Instance**

```python
response = ec2_resource.create_instances(
    ImageId='ami-0abcdef1234567890',  # AMI ID
    MinCount=1,
    MaxCount=1,
    InstanceType='t2.micro',
    KeyName='my-key-pair',
    SecurityGroupIds=['sg-0abc12345'],
    SubnetId='subnet-0ab1234'
)

instance = response[0]
print(f"Launched instance with ID: {instance.id}")
```

**Key parameters**: `ImageId`, `InstanceType`, `KeyName`, `SecurityGroupIds`, `SubnetId`.

---

### **3. List All EC2 Instances**

```python
for instance in ec2_resource.instances.all():
    print(f"ID: {instance.id}, State: {instance.state['Name']}, Type: {instance.instance_type}")
```

**Using Client:**

```python
response = ec2_client.describe_instances()
for reservation in response['Reservations']:
    for instance in reservation['Instances']:
        print(f"ID: {instance['InstanceId']}, State: {instance['State']['Name']}")
```

---

### **4. Start/Stop/Terminate Instances**

```python
instance_id = 'i-0abc1234'

# Start
ec2_client.start_instances(InstanceIds=[instance_id])

# Stop
ec2_client.stop_instances(InstanceIds=[instance_id])

# Terminate
ec2_client.terminate_instances(InstanceIds=[instance_id])
```

> **Tip:** Always check instance state before starting/stopping to avoid errors.

---

### **5. Reboot an Instance**

```python
ec2_client.reboot_instances(InstanceIds=[instance_id])
```

---

### **6. Get Instance Status**

```python
instance = ec2_resource.Instance('i-0abc1234')
print(instance.state['Name'])  # running, stopped, pending, terminated
```

**Check multiple instances:**

```python
statuses = ec2_client.describe_instance_status(InstanceIds=['i-0abc1234'])
print(statuses)
```

---

### **7. Tagging an Instance**

```python
instance.create_tags(Tags=[{'Key': 'Environment', 'Value': 'Dev'}])
```

> Tags help organize instances by purpose or project.

---

### **8. Example: Filtering Instances by State**

```python
running_instances = ec2_resource.instances.filter(Filters=[{'Name': 'instance-state-name', 'Values': ['running']}])
for instance in running_instances:
    print(instance.id, instance.instance_type)
```

---

### **9. Best Practices**

* Use **resource** when working with objects; client for **API calls**.
* Always handle exceptions (`try-except`) for operations like start/stop.
* Avoid hardcoding sensitive info; use **IAM roles** or environment variables.
* Always **terminate** unused instances to avoid unnecessary costs.

---

## **Practical Exam Question**

**Question:**
Write a Python script using Boto3 that:

1. Lists all EC2 instances in your account.
2. Filters only running instances.
3. Stops all running instances and prints their IDs.
4. Creates a tag `StoppedBy` with value `ExamScript` on each stopped instance.

---

**Answer (Python Code):**

```python
import boto3

# Initialize EC2 resource
ec2 = boto3.resource('ec2', region_name='us-east-1')

# 1 & 2. List all running instances
running_instances = ec2.instances.filter(Filters=[{'Name': 'instance-state-name', 'Values': ['running']}])

# 3. Stop each running instance
for instance in running_instances:
    print(f"Stopping instance: {instance.id}")
    instance.stop()
    instance.wait_until_stopped()  # Wait until the instance is actually stopped

    # 4. Tag the stopped instance
    instance.create_tags(Tags=[{'Key': 'StoppedBy', 'Value': 'ExamScript'}])
    print(f"Tagged instance {instance.id} with 'StoppedBy: ExamScript'")

print("All running instances stopped and tagged successfully.")
```

**Expected Output Example:**

```
Stopping instance: i-0abc1234
Tagged instance i-0abc1234 with 'StoppedBy: ExamScript'
Stopping instance: i-0def5678
Tagged instance i-0def5678 with 'StoppedBy: ExamScript'
All running instances stopped and tagged successfully.
```

---

✅ This covers **all common EC2 instance operations** that DevOps engineers are expected to know for practical exams or interviews.

---

If you want, I can also make a **table of all EC2 operations with Boto3, including client vs resource methods, parameters, and examples**. It’s very handy for quick revision.

Do you want me to make that?
