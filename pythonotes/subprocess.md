Here are **complete Python `subprocess` module notes with DevOps examples** — one of the most important modules for automation and scripting 👇

---

## ⚙️ **Python `subprocess` Module (For DevOps)**

The `subprocess` module allows you to **run shell/Linux commands directly from Python** — useful for automation, deployment, monitoring, backups, etc.

---

### ✅ **1️⃣ Import the module**

```python
import subprocess
```

---

### ✅ **2️⃣ Run a simple command**

```python
subprocess.run(["ls", "-l"])
```

🧠 **Use case:**
List files on a remote build or deployment server.

---

### ✅ **3️⃣ Capture output**

```python
result = subprocess.run(["uname", "-a"], capture_output=True, text=True)
print("Output:", result.stdout)
```

📘 **Parameters:**

* `capture_output=True` → captures both stdout and stderr
* `text=True` → converts bytes to string automatically

🧠 **Use case:**
Collect system info or command output for logging.

---

### ✅ **4️⃣ Handle errors safely**

```python
result = subprocess.run(["cat", "nofile.txt"], capture_output=True, text=True)
print("Error:", result.stderr)
```

🧠 **Use case:**
Log errors from failed deployments or missing files.

---

### ✅ **5️⃣ Check command success**

```python
result = subprocess.run(["ls", "/tmp"], capture_output=True, text=True)
if result.returncode == 0:
    print("Command succeeded")
else:
    print("Command failed")
```

🧠 **Use case:**
Check status of shell commands in automation scripts.

---

### ✅ **6️⃣ Using `check=True`**

```python
subprocess.run(["false"], check=True)
```

⚠️ This will raise an exception if the command fails:

```
subprocess.CalledProcessError: Command '['false']' returned non-zero exit status 1.
```

🧠 **Use case:**
Stop script execution immediately if a deployment step fails.

---

### ✅ **7️⃣ Get both stdout & stderr together**

```python
result = subprocess.run(["df", "-h"], capture_output=True, text=True)
print(result.stdout)
print(result.stderr)
```

🧠 **Use case:**
Get both success and failure logs for analysis.

---

### ✅ **8️⃣ Run command in shell mode**

```python
subprocess.run("echo $HOME", shell=True)
```

🧠 **Use case:**
Run shell-based commands like pipes (`|`), redirections (`>`), or environment variables.

```python
subprocess.run("ls -l | grep log", shell=True)
```

⚠️ **Security Tip:**
Avoid `shell=True` with user input → risk of shell injection.

---

### ✅ **9️⃣ Get command output (using `check_output`)**

```python
output = subprocess.check_output(["hostname"], text=True)
print("Hostname:", output.strip())
```

🧠 **Use case:**
Capture command output directly (useful in monitoring scripts).

---

### ✅ **🔟 Pass environment variables**

```python
import os

my_env = os.environ.copy()
my_env["ENV"] = "production"

subprocess.run(["printenv", "ENV"], env=my_env)
```

🧠 **Use case:**
Pass dynamic environment variables during CI/CD jobs.

---

### ✅ **11️⃣ Run background process**

```python
proc = subprocess.Popen(["ping", "google.com", "-c", "3"])
print("Process running in background...")
proc.wait()
print("Completed.")
```

🧠 **Use case:**
Run long-running tasks (like backup or sync) in background.

---

### ✅ **12️⃣ Redirect output to a file**

```python
with open("system_info.txt", "w") as f:
    subprocess.run(["uname", "-a"], stdout=f)
```

🧠 **Use case:**
Save command output (logs, system info, etc.) to a file.

---

### ✅ **13️⃣ Read command output line by line (streaming)**

```python
proc = subprocess.Popen(["ping", "-c", "3", "google.com"], stdout=subprocess.PIPE, text=True)

for line in proc.stdout:
    print(line.strip())
```

🧠 **Use case:**
Live stream logs during deployments or builds.

---

### ✅ **14️⃣ Example: Deployment Automation**

```python
import subprocess
from datetime import datetime

def deploy_app():
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    print(f"[{timestamp}] Starting deployment...")

    cmds = [
        ["git", "pull"],
        ["docker", "build", "-t", "myapp:latest", "."],
        ["docker", "compose", "up", "-d"]
    ]

    for cmd in cmds:
        result = subprocess.run(cmd, capture_output=True, text=True)
        if result.returncode == 0:
            print(f"✅ {' '.join(cmd)} succeeded")
        else:
            print(f"❌ {' '.join(cmd)} failed\n{result.stderr}")
            break

deploy_app()
```

🧠 **DevOps use case:**
Automate deployment pipeline steps (Git → Docker → Run).

---

### ✅ **15️⃣ Example: System Monitoring Script**

```python
import subprocess

def check_disk_usage():
    result = subprocess.run(["df", "-h", "/"], capture_output=True, text=True)
    print("Disk Usage Info:\n", result.stdout)

check_disk_usage()
```

🧠 **Use case:**
Integrate with monitoring scripts or alerts.

---

## 🧩 **Summary Table**

| Method                | Description                  | Example                         |
| --------------------- | ---------------------------- | ------------------------------- |
| `subprocess.run()`    | Run a command                | `run(["ls"])`                   |
| `capture_output=True` | Capture stdout/stderr        | `result.stdout`                 |
| `check=True`          | Raise error if command fails | `run(["false"], check=True)`    |
| `check_output()`      | Return command output        | `check_output(["hostname"])`    |
| `Popen()`             | Run background process       | `Popen(["ping", "8.8.8.8"])`    |
| `env=`                | Pass custom environment vars | `run(["printenv"], env=my_env)` |

---

Would you like me to make a **DevOps subprocess automation cheat sheet (PDF)** summarizing all the examples and commands?
