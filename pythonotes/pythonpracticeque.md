Perfect 👏 — here’s a curated list of **DevOps interview practical Python questions** that focus on **real-world automation tasks** you’ll actually face in DevOps work.

Each question includes what the interviewer expects and a short working example.

---

## 🐍 **DevOps Python Practical Interview Questions**

---

### 🔹 **1. Run a shell command and capture its output**

**Question:**
Write a Python script to execute `ls -l /tmp` and print the output.

**Answer:**

```python
import subprocess

result = subprocess.run(["ls", "-l", "/tmp"], capture_output=True, text=True)
print(result.stdout)
```

🧠 *Used to automate Linux operations or CI/CD jobs.*

---

### 🔹 **2. Check if a Linux service is running**

**Question:**
Write Python code to check if the `nginx` service is active.

**Answer:**

```python
import subprocess

service = "nginx"
status = subprocess.run(["systemctl", "is-active", service], capture_output=True, text=True)

if status.stdout.strip() == "active":
    print(f"{service} is running ✅")
else:
    print(f"{service} is not running ❌")
```

🧠 *Used for monitoring or pre-deployment checks.*

---

### 🔹 **3. Create a backup of a directory as a ZIP**

**Question:**
Backup `/var/lib/jenkins` to `/tmp/backups` with timestamp.

**Answer:**

```python
import shutil
from datetime import datetime
import os

src = "/var/lib/jenkins"
dest = "/tmp/backups"

os.makedirs(dest, exist_ok=True)
timestamp = datetime.now().strftime("%Y-%m-%d_%H-%M-%S")
backup_file = f"{dest}/jenkins_backup_{timestamp}"

shutil.make_archive(backup_file, 'zip', src)
print(f"Backup created: {backup_file}.zip ✅")
```

🧠 *Common DevOps scripting for scheduled backups.*

---

### 🔹 **4. Read a log file and count “error” lines**

**Question:**
Count how many times the word “error” appears in `/var/log/syslog`.

**Answer:**

```python
count = 0
with open("/var/log/syslog", "r") as f:
    for line in f:
        if "error" in line.lower():
            count += 1
print("Total error lines:", count)
```

🧠 *Useful for log monitoring scripts.*

---

### 🔹 **5. Check disk usage and alert if >80%**

**Question:**
Write a Python script that checks `/` disk usage.

**Answer:**

```python
import shutil

total, used, free = shutil.disk_usage("/")
usage = (used / total) * 100

if usage > 80:
    print(f"⚠️ Warning! Disk usage is {usage:.2f}%")
else:
    print(f"✅ Disk usage OK: {usage:.2f}%")
```

🧠 *Used for system health monitoring.*

---

### 🔹 **6. Ping a list of servers**

**Question:**
Ping multiple servers from a file and show which are reachable.

**Answer:**

```python
import subprocess

servers = ["google.com", "amazon.com", "example.local"]

for server in servers:
    result = subprocess.run(["ping", "-c", "2", server], stdout=subprocess.DEVNULL)
    if result.returncode == 0:
        print(f"{server} is reachable ✅")
    else:
        print(f"{server} is unreachable ❌")
```

🧠 *Tests connectivity in CI/CD or network scripts.*

---

### 🔹 **7. Read environment variable**

**Question:**
How do you read the environment variable `ENV` and set a default value?

**Answer:**

```python
import os

env = os.getenv("ENV", "dev")
print("Current environment:", env)
```

🧠 *Common in Docker, Jenkins, and deployment automation.*

---

### 🔹 **8. Monitor a log file like `tail -f`**

**Question:**
Implement a simple log tail in Python.

**Answer:**

```python
import time

with open("/var/log/syslog", "r") as file:
    file.seek(0, 2)
    while True:
        line = file.readline()
        if not line:
            time.sleep(0.5)
            continue
        print(line.strip())
```

🧠 *Used for live log monitoring.*

---

### 🔹 **9. Copy files between directories**

**Question:**
Copy all `.log` files from `/var/log` to `/tmp/log_backup`.

**Answer:**

```python
import os, shutil

src = "/var/log"
dst = "/tmp/log_backup"
os.makedirs(dst, exist_ok=True)

for file in os.listdir(src):
    if file.endswith(".log"):
        shutil.copy(os.path.join(src, file), dst)
```

🧠 *Automated file management for servers.*

---

### 🔹 **10. List all running processes (Linux)**

**Question:**
Get all running processes and save them to a file.

**Answer:**

```python
import subprocess

result = subprocess.run(["ps", "-ef"], capture_output=True, text=True)
with open("/tmp/process_list.txt", "w") as f:
    f.write(result.stdout)
print("Process list saved to /tmp/process_list.txt")
```

🧠 *Helps in creating system reports or debugging.*

---

## 🧪 **Bonus: Mini Project Interview Task**

**Scenario:**
Write a Python script that:

* Reads a list of directories from a file (`dirs.txt`)
* Creates ZIP backups for each directory
* Stores them in `/tmp/backups`

**Answer:**

```python
import shutil, os
from datetime import datetime

backup_dir = "/tmp/backups"
os.makedirs(backup_dir, exist_ok=True)

with open("dirs.txt", "r") as f:
    dirs = [d.strip() for d in f]

for d in dirs:
    if os.path.exists(d):
        name = os.path.basename(d.strip("/"))
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        zip_name = f"{backup_dir}/{name}_{timestamp}"
        shutil.make_archive(zip_name, "zip", d)
        print(f"✅ Backup created for {d}")
    else:
        print(f"❌ Directory not found: {d}")
```

🧠 *This simulates a real automation script for backups — a **favorite DevOps interview task**.*

---

Would you like me to give you a **mock DevOps Python test (10 questions)** where you can try solving and I’ll give answers after?
(It’s great for practice before interviews.)
