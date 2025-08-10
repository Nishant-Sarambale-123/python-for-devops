Alright, let’s go into **Intermediate Python (Automation Ready)** with detailed notes, examples, and DevOps-friendly tips.
These will help you bridge from **basic Python** to **automation scripting**.

---

## **1. File Operations**

### **Reading/Writing Text Files**

```python
# Write to a file
with open("example.txt", "w") as f:
    f.write("Hello DevOps!\n")

# Append to a file
with open("example.txt", "a") as f:
    f.write("Appending text...\n")

# Read entire file
with open("example.txt", "r") as f:
    content = f.read()

# Read line by line
with open("example.txt", "r") as f:
    for line in f:
        print(line.strip())
```

**Best Practice:** Always use `with open(...)` — it auto-closes the file.

---

### **Reading/Writing CSV Files**

```python
import csv

# Writing CSV
with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Role"])
    writer.writerow(["Nishant", "DevOps Engineer"])

# Reading CSV
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

---

### **JSON Parsing**

```python
import json

# Writing JSON
data = {"name": "Nishant", "role": "DevOps"}
with open("data.json", "w") as f:
    json.dump(data, f, indent=4)

# Reading JSON
with open("data.json", "r") as f:
    data_loaded = json.load(f)
```

---

### **YAML Parsing** (requires `PyYAML`)

```python
import yaml

# Writing YAML
data = {"name": "Nishant", "role": "DevOps"}
with open("data.yaml", "w") as f:
    yaml.dump(data, f)

# Reading YAML
with open("data.yaml", "r") as f:
    data_loaded = yaml.safe_load(f)
```

---

## **2. Modules & Packages**

### **Importing Modules**

```python
import os
from math import sqrt
import sys as system  # alias
```

### **Creating a Custom Module**

* File: `mymodule.py`

  ```python
  def greet(name):
      return f"Hello {name}"
  ```
* Usage:

  ```python
  import mymodule
  print(mymodule.greet("Nishant"))
  ```

### **Popular DevOps Libraries**

* **`os`** → File & directory operations, environment vars.
* **`sys`** → System-specific parameters, arguments.
* **`subprocess`** → Run shell commands.

  ```python
  import subprocess
  result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
  print(result.stdout)
  ```
* **`shutil`** → Copy, move, delete files/directories.

  ```python
  import shutil
  shutil.copy("source.txt", "backup.txt")
  ```

---

## **3. Error Handling**

### **Basic try-except**

```python
try:
    num = int("abc")
except ValueError as e:
    print(f"Error: {e}")
```

### **try-except-finally**

```python
try:
    f = open("file.txt")
except FileNotFoundError:
    print("File not found!")
finally:
    print("Execution finished.")
```

### **Custom Exceptions**

```python
class MyError(Exception):
    pass

try:
    raise MyError("Something went wrong")
except MyError as e:
    print(e)
```

---

## **4. Environment Variables**

### **Using `os.environ`**

```python
import os
os.environ["MY_VAR"] = "value"
print(os.environ.get("MY_VAR"))
```

### **Handling `.env` Files** (with `python-dotenv`)

```python
from dotenv import load_dotenv
import os

load_dotenv()  # Loads from .env
print(os.getenv("API_KEY"))
```

---

## **5. Virtual Environments**

### **Creating & Activating venv**

```bash
# Create
python3 -m venv myenv

# Activate (Linux/Mac)
source myenv/bin/activate

# Activate (Windows)
myenv\Scripts\activate
```

### **Installing packages**

```bash
pip install requests
pip freeze > requirements.txt
pip install -r requirements.txt
```

---

## **6. Date & Time**

### **Basic datetime usage**

```python
from datetime import datetime

now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))
```

### **Time Zone Handling**

```python
from datetime import datetime
import pytz

utc_time = datetime.now(pytz.UTC)
india_time = utc_time.astimezone(pytz.timezone("Asia/Kolkata"))
print(india_time)
```

---

I can also make you a **DevOps Python Automation Toolkit sheet** where I combine:

* File handling templates
* Shell command execution
* YAML/JSON parsing
* Env var handling
  so you can copy-paste and modify for scripts.

Do you want me to prepare that next? That would make your automation work super fast.
