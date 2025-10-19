Perfect 👏 Nishant!
Below is a **complete, detailed set of notes** on
➡️ **Python Intermediate Concepts for DevOps**
with **real DevOps automation examples** for each topic.

These are the most **commonly used** concepts in **infrastructure automation, CI/CD, configuration management, and monitoring scripts**.

---

# ⚙️ **2. Intermediate Python Concepts for DevOps**

---

## 🧩 1. Working with OS Module (`os`, `sys`, `platform`)

### **a) `os` module**

Used to interact with the **Operating System** — managing files, directories, permissions, environment variables, etc.

```python
import os

# Get current working directory
print(os.getcwd())

# List files in directory
print(os.listdir("/var/log"))

# Run shell command
os.system("systemctl status nginx")

# Check environment variable
print(os.environ.get("HOME"))
```

✅ **DevOps Example:**
Automatically clean up temp folders and logs.

```python
import os

log_path = "/var/log/app"
for file in os.listdir(log_path):
    if file.endswith(".old"):
        os.remove(os.path.join(log_path, file))
        print(f"Deleted old log: {file}")
```

---

### **b) `sys` module**

Used to interact with the **Python runtime environment**.

```python
import sys

print(sys.version)
print(sys.platform)
print(sys.path)
```

✅ **DevOps Example:**
Check if the script is running on the expected OS.

```python
import sys
if sys.platform != "linux":
    sys.exit("This script must run on Linux only")
```

---

### **c) `platform` module**

Used to identify **OS name, version, and architecture**.

```python
import platform
print(platform.system())      # Linux
print(platform.release())     # 5.15.0-78
print(platform.machine())     # x86_64
```

✅ **DevOps Example:**
Detect the OS before installing packages.

```python
import platform, os

if platform.system() == "Linux":
    os.system("sudo apt update && sudo apt install nginx -y")
elif platform.system() == "Windows":
    os.system("choco install nginx")
```

---

## 🧾 2. Subprocess Module (Running Shell Commands Safely)

`subprocess` is the **recommended** module for running system commands
(instead of `os.system()`).

```python
import subprocess

result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print(result.stdout)
```

✅ **DevOps Example:**
Check Nginx service status.

```python
import subprocess

cmd = ["systemctl", "is-active", "nginx"]
result = subprocess.run(cmd, capture_output=True, text=True)
if result.stdout.strip() == "active":
    print("✅ Nginx is running")
else:
    print("❌ Nginx is not running")
```

---

## 🧠 3. Logging and Error Tracking

Use the `logging` module to record script events instead of print statements.

```python
import logging

logging.basicConfig(filename="app.log", level=logging.INFO,
                    format="%(asctime)s - %(levelname)s - %(message)s")

try:
    x = 10 / 0
except Exception as e:
    logging.error("Error occurred: %s", e)
```

✅ **DevOps Example:**
Track automation success/failure logs for deployments.

```python
import logging, os

logging.basicConfig(filename="deploy.log", level=logging.INFO)

if os.path.exists("/opt/app"):
    logging.info("App directory found, continuing deployment.")
else:
    logging.warning("App directory missing, creating...")
    os.makedirs("/opt/app")
```

---

## ⚙️ 4. JSON / YAML Handling (Configuration Files)

These are used for **config management**, **IaC**, and **API automation**.

### **a) JSON Handling**

```python
import json

# Read JSON file
with open("config.json") as f:
    data = json.load(f)
print(data["environment"])

# Write JSON
data["version"] = "2.0"
with open("config.json", "w") as f:
    json.dump(data, f, indent=4)
```

✅ **DevOps Example:**
Modify a config file dynamically before deployment.

---

### **b) YAML Handling**

```python
import yaml

with open("config.yaml") as f:
    data = yaml.safe_load(f)

data["replicas"] = 5

with open("config.yaml", "w") as f:
    yaml.dump(data, f)
```

✅ **DevOps Example:**
Update Kubernetes YAML manifests or Ansible inventory.

---

## 🌍 5. Environment Variables (`os.environ`)

Used to store sensitive information like **API keys, credentials, or environment name**.

```python
import os

# Read
print(os.environ.get("AWS_PROFILE"))

# Set
os.environ["DEPLOY_ENV"] = "production"
print(os.environ["DEPLOY_ENV"])
```

✅ **DevOps Example:**
Switch between staging and production environment dynamically.

```python
import os

env = os.environ.get("DEPLOY_ENV", "staging")
if env == "production":
    print("Deploying to PRODUCTION")
else:
    print("Deploying to STAGING")
```

---

## 🕒 6. Date and Time Operations (`datetime` module)

Used for **log timestamps, backup filenames, or report generation**.

```python
from datetime import datetime, timedelta

now = datetime.now()
print("Current Time:", now.strftime("%Y-%m-%d %H:%M:%S"))

yesterday = now - timedelta(days=1)
print("Yesterday:", yesterday)
```

✅ **DevOps Example:**
Generate backup file with timestamp.

```python
from datetime import datetime
import shutil

filename = f"backup_{datetime.now().strftime('%Y%m%d_%H%M%S')}.tar.gz"
shutil.make_archive(filename, 'gztar', '/opt/app')
print(f"Backup created: {filename}")
```

---

## 🔍 7. Regular Expressions (`re` module)

Used for **log parsing**, **pattern matching**, and **validations**.

```python
import re

log = "Error: CPU usage 95%"
match = re.search(r"CPU usage (\d+)%", log)
if match:
    print("CPU:", match.group(1))
```

✅ **DevOps Example:**
Extract failed services from a log file.

```python
import re

with open("/var/log/syslog") as f:
    for line in f:
        if re.search(r"failed|error", line, re.IGNORECASE):
            print(line.strip())
```

---

## 🧰 8. Argument Parsing (`argparse` module)

Used to pass **command-line arguments** to Python scripts
(similar to `bash` parameters).

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("--env", help="Environment name")
args = parser.parse_args()

print(f"Deploying to {args.env} environment")
```

✅ **DevOps Example:**
Use one script for multiple environments.

```bash
python deploy.py --env production
python deploy.py --env staging
```

---

## 🧩 9. Virtual Environments & Dependencies

### **Create virtual environment**

```bash
python3 -m venv venv
source venv/bin/activate
```

### **Install packages**

```bash
pip install boto3 requests pyyaml
```

### **Save dependencies**

```bash
pip freeze > requirements.txt
```

### **Install from requirements**

```bash
pip install -r requirements.txt
```

✅ **DevOps Use Case:**
Create isolated environments for automation tools (Ansible scripts, Flask dashboards, etc.)
to avoid dependency conflicts.

---

## 🧾 Summary Table

| Concept         | Module                  | DevOps Use Case                     |
| --------------- | ----------------------- | ----------------------------------- |
| OS interaction  | `os`, `sys`, `platform` | File ops, env detection, automation |
| Shell commands  | `subprocess`            | Run Linux commands safely           |
| Logging         | `logging`               | Debug and record automation tasks   |
| Config handling | `json`, `yaml`          | Manage IaC, pipelines, manifests    |
| Env variables   | `os.environ`            | Store credentials/configs securely  |
| Date/time       | `datetime`              | Backups, timestamps, reporting      |
| Regex           | `re`                    | Parse logs, extract metrics         |
| Argparse        | `argparse`              | CLI scripts for deployments         |
| Virtual env     | `venv`, `pip`           | Isolate dependencies for automation |

---

Would you like me to make a **PDF cheat sheet** version of these “Python for DevOps – Intermediate Notes” (formatted with examples and summary tables)?
It’s perfect for **quick revision before interviews**.
