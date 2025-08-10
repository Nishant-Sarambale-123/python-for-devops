Here’s a **detailed breakdown** of those **DevOps-oriented Python skills**, with examples so you know exactly what each means and why it’s useful in DevOps work.

---

## **1. System Administration**

### **a) Running shell commands with `subprocess`**

* Used to run Linux/Windows commands from Python scripts.
* Example:

```python
import subprocess
result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print(result.stdout)
```

✅ Use case: Automating server tasks (deployments, service restarts).

---

### **b) File/Directory management with `os` and `shutil`**

* `os` → basic file & directory operations.
* `shutil` → high-level file operations (copy, move, delete).
* Example:

```python
import os, shutil
os.mkdir("logs")  # Create folder
shutil.copy("app.log", "logs/backup.log")  # Copy file
```

✅ Use case: Backup logs, manage config files, clean temp folders.

---

## **2. Networking**

### **a) Working with `socket`**

* Used to create network connections (client/server).
* Example (simple TCP client):

```python
import socket
s = socket.socket()
s.connect(("example.com", 80))
s.send(b"GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
print(s.recv(1024))
s.close()
```

✅ Use case: Build custom monitoring tools or health checks.

---

### **b) HTTP requests with `requests` library**

* For calling APIs over HTTP/HTTPS.
* Example:

```python
import requests
response = requests.get("https://api.github.com")
print(response.json())
```

✅ Use case: Integrate with DevOps tools (Jenkins, GitHub, GitLab APIs).

---

## **3. Cloud & API Automation**

### **a) AWS automation with `boto3`**

* AWS SDK for Python.
* Example: List S3 buckets

```python
import boto3
s3 = boto3.client("s3")
for bucket in s3.list_buckets()["Buckets"]:
    print(bucket["Name"])
```

✅ Use case: Automate EC2, S3, IAM, Lambda operations.

---

### **b) Kubernetes automation with `python-kubernetes`**

* Interact with Kubernetes cluster programmatically.
* Example: List pods in a namespace

```python
from kubernetes import client, config
config.load_kube_config()
v1 = client.CoreV1Api()
for pod in v1.list_namespaced_pod(namespace="default").items:
    print(pod.metadata.name)
```

✅ Use case: Deployments, scaling, pod health checks.

---

### **c) REST API calls & parsing JSON responses**

* Combine `requests` + `json` to work with APIs.
* Example:

```python
import requests
data = requests.get("https://jsonplaceholder.typicode.com/posts/1").json()
print(data["title"])
```

✅ Use case: Trigger CI/CD pipelines, fetch status, integrate alerts.

---

## **4. Configuration Management**

### **a) Parsing YAML with `PyYAML`**

* Used for reading config files like Kubernetes YAML.
* Example:

```python
import yaml
with open("config.yaml") as f:
    config = yaml.safe_load(f)
print(config["version"])
```

✅ Use case: Modify deployment configs before applying them.

---

### **b) Editing config files programmatically**

* Modify `.conf`, `.ini`, `.yaml` files with Python.
* Example:

```python
config["version"] = "2.0"
with open("config.yaml", "w") as f:
    yaml.dump(config, f)
```

✅ Use case: Dynamic config updates before deployment.

---

## **5. Log Handling**

### **a) Reading log files**

* Process server logs in real-time or batch mode.
* Example:

```python
with open("/var/log/syslog") as f:
    for line in f:
        if "ERROR" in line:
            print(line)
```

✅ Use case: Monitoring, troubleshooting.

---

### **b) Regex filtering with `re` module**

* Extract patterns from text.
* Example:

```python
import re
log = "ERROR 2025-08-10 Connection failed"
match = re.search(r"ERROR\s+\d{4}-\d{2}-\d{2}", log)
if match:
    print("Error log found:", match.group())
```

✅ Use case: Find IP addresses, timestamps, error codes in logs.

---

If you want, I can turn this into a **structured DevOps Python learning roadmap** — from beginner to advanced — so you can master these skills in a logical order. That way, you’ll cover exactly what’s needed for interviews and real projects.
