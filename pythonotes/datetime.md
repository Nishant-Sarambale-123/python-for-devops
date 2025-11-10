Here are **Python `datetime` module notes with examples useful for DevOps engineers** — written clearly and practically 👇

---

## 🕒 **Python `datetime` Module (For DevOps)**

The `datetime` module is used for **working with dates and times**, such as logging, timestamps, automation scripts, backups, or scheduling in DevOps tasks.

---

### ✅ **1. Import the module**

```python
import datetime
```

---

### ✅ **2. Get current date and time**

```python
from datetime import datetime

now = datetime.now()
print("Current Date & Time:", now)
print("Only Date:", now.date())
print("Only Time:", now.time())
```

🧠 **DevOps use case:**
Add timestamps in automation scripts or log files.

```python
with open("deploy_log.txt", "a") as f:
    f.write(f"Deployment started at: {datetime.now()}\n")
```

---

### ✅ **3. Get current UTC time**

```python
from datetime import datetime, timezone

utc_time = datetime.now(timezone.utc)
print("UTC Time:", utc_time)
```

🧠 **Use case:**
For distributed systems and cloud logs, use UTC to keep timestamps consistent across servers.

---

### ✅ **4. Get today’s date**

```python
from datetime import date

today = date.today()
print("Today:", today)
```

🧠 **Use case:**
Use date in filenames (e.g., backups or reports).

```python
backup_filename = f"db_backup_{date.today()}.sql"
print(backup_filename)
```

---

### ✅ **5. Format Date/Time (strftime)**

```python
now = datetime.now()
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
print("Formatted:", formatted)
```

📘 **Common format codes:**

| Code | Meaning         | Example |
| ---- | --------------- | ------- |
| `%Y` | Year (4 digits) | 2025    |
| `%m` | Month (01–12)   | 11      |
| `%d` | Day (01–31)     | 10      |
| `%H` | Hour (00–23)    | 15      |
| `%M` | Minute (00–59)  | 45      |
| `%S` | Second (00–59)  | 22      |

🧠 **Use case:**
Used in CI/CD logs, reports, tagging Docker images with timestamps.

```python
tag = datetime.now().strftime("%Y%m%d%H%M%S")
print(f"docker build -t myapp:{tag} .")
```

---

### ✅ **6. Parse string to datetime (strptime)**

```python
from datetime import datetime

dt_string = "2025-11-10 14:30:00"
dt_object = datetime.strptime(dt_string, "%Y-%m-%d %H:%M:%S")
print("Converted:", dt_object)
```

🧠 **Use case:**
Parse timestamps from log files for analysis or comparison.

---

### ✅ **7. Add or subtract time (timedelta)**

```python
from datetime import datetime, timedelta

now = datetime.now()
future = now + timedelta(days=7)
past = now - timedelta(hours=3)

print("After 7 days:", future)
print("3 hours ago:", past)
```

🧠 **Use case:**

* Schedule tasks (e.g., next maintenance window).
* Clean up old log files (older than X days).

```python
import os

log_time = datetime.now() - timedelta(days=30)
print(f"Delete logs older than {log_time}")
```

---

### ✅ **8. Compare two dates**

```python
from datetime import date

d1 = date(2025, 11, 1)
d2 = date(2025, 11, 10)

if d2 > d1:
    print("Second date is after the first date.")
```

🧠 **Use case:**
Check if certificates, passwords, or tokens are expired.

---

### ✅ **9. Measure script execution time**

```python
import datetime
start = datetime.datetime.now()

# Simulate task
for i in range(1000000):
    pass

end = datetime.datetime.now()
print("Execution time:", end - start)
```

🧠 **Use case:**
Monitor how long a deployment or backup takes.

---

### ✅ **10. Timezones (with `pytz` – optional)**

```python
from datetime import datetime
import pytz

india = pytz.timezone('Asia/Kolkata')
now_india = datetime.now(india)
print("India Time:", now_india)
```

🧠 **Use case:**
Convert UTC logs to your local timezone for debugging.

---

## ⚙️ **Quick DevOps Example: Timestamped Log File**

```python
from datetime import datetime

def log_event(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open("pipeline.log", "a") as log:
        log.write(f"[{timestamp}] {message}\n")

log_event("Build started")
log_event("Deployment completed successfully")
```

📄 **Output:**

```
[2025-11-10 14:15:10] Build started
[2025-11-10 14:20:22] Deployment completed successfully
```

---

### 🧩 Summary

| Function         | Description               | Example                                       |
| ---------------- | ------------------------- | --------------------------------------------- |
| `datetime.now()` | Current local date & time | `2025-11-10 15:30:00`                         |
| `date.today()`   | Current date only         | `2025-11-10`                                  |
| `strftime()`     | Format date/time          | `now.strftime("%Y-%m-%d")`                    |
| `strptime()`     | Parse string to datetime  | `datetime.strptime("2025-11-10", "%Y-%m-%d")` |
| `timedelta()`    | Add/Subtract time         | `now + timedelta(days=7)`                     |

---

Would you like me to make a **one-page summarized cheat sheet (PDF)** version of this for quick DevOps reference?
