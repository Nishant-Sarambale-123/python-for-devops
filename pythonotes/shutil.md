Here’s a **detailed and complete note on the `shutil` module in Python** — perfect for DevOps, automation, and interview preparation.

---

# 🐍 Python `shutil` Module – Detailed Notes

## 📘 Overview

* `shutil` (Shell Utilities) is a **standard Python library** used for **high-level file operations**.
* It provides utilities to **copy, move, delete, and archive files and directories**.
* It builds on top of the lower-level `os` module, which handles basic filesystem operations.

---

## 📦 Importing `shutil`

```python
import shutil
```

---

## 🔹 Commonly Used Functions in `shutil`

### 1. **Copying Files**

#### a. `shutil.copy(src, dst)`

* Copies the **contents of a file** from `src` to `dst`.
* Metadata (like permissions, timestamps) **is not preserved**.

```python
shutil.copy("file1.txt", "backup/file1.txt")
```

#### b. `shutil.copy2(src, dst)`

* Same as `copy()`, but **preserves metadata** (timestamps, permissions).
* Similar to Linux command `cp -p`.

```python
shutil.copy2("data.txt", "archive/data.txt")
```

#### c. `shutil.copyfile(src, dst)`

* Copies **contents only** (no permissions or metadata).
* Destination must be a **file path**, not a directory.

```python
shutil.copyfile("log.txt", "log_backup.txt")
```

#### d. `shutil.copyfileobj(src_file, dst_file, length=0)`

* Copies contents between **two open file objects**.

```python
with open("a.txt", "rb") as fsrc, open("b.txt", "wb") as fdst:
    shutil.copyfileobj(fsrc, fdst)
```

---

### 2. **Moving and Renaming Files**

#### `shutil.move(src, dst)`

* Moves or renames files/directories.
* Works across file systems.
* Similar to Linux command `mv`.

```python
shutil.move("temp/report.txt", "reports/final_report.txt")
```

---

### 3. **Deleting Files and Directories**

#### a. `shutil.rmtree(path)`

* Removes an entire directory tree (recursively).
* ⚠️ **Use with caution** – it deletes everything inside!

```python
shutil.rmtree("/tmp/testdir")
```

#### b. To remove only a single file:

Use the `os` module instead:

```python
import os
os.remove("file.txt")
```

---

### 4. **Directory Operations**

#### a. `shutil.copytree(src, dst, dirs_exist_ok=False)`

* Recursively copies a **directory tree** from `src` to `dst`.
* If `dirs_exist_ok=True`, it overwrites existing directories (Python 3.8+).

```python
shutil.copytree("project", "project_backup", dirs_exist_ok=True)
```

#### b. `shutil.ignore_patterns(*patterns)`

* Used with `copytree()` to **ignore certain files/folders**.

```python
ignore = shutil.ignore_patterns('*.pyc', '__pycache__')
shutil.copytree("src", "dest", ignore=ignore)
```

---

### 5. **Disk Usage**

#### `shutil.disk_usage(path)`

* Returns total, used, and free space on the disk containing `path`.
* Returns a **named tuple**: `(total, used, free)`

```python
usage = shutil.disk_usage("/")
print(f"Total: {usage.total // (2**30)} GB")
print(f"Used: {usage.used // (2**30)} GB")
print(f"Free: {usage.free // (2**30)} GB")
```

---

### 6. **Archiving (Compressing / Extracting)**

#### a. `shutil.make_archive(base_name, format, root_dir)`

* Creates a compressed archive (`zip`, `tar`, `gztar`, etc.)
* Equivalent to Linux commands `tar` or `zip`.

```python
shutil.make_archive("backup_project", "zip", "project_dir")
```

👉 Output: `backup_project.zip`

**Common formats:**

| Format | Description   | Example Output |
| ------ | ------------- | -------------- |
| zip    | ZIP archive   | `data.zip`     |
| tar    | Tarball       | `data.tar`     |
| gztar  | gzip tarball  | `data.tar.gz`  |
| bztar  | bzip2 tarball | `data.tar.bz2` |
| xztar  | xz tarball    | `data.tar.xz`  |

#### b. `shutil.unpack_archive(filename, extract_dir=None, format=None)`

* Extracts an archive file to a directory.
* Auto-detects the format if not given.

```python
shutil.unpack_archive("backup_project.zip", "restored_project")
```

---

### 7. **Temporary Directories and Files**

Although not directly in `shutil`, it works closely with the `tempfile` module.

```python
import tempfile

with tempfile.TemporaryDirectory() as tmpdir:
    print("Temporary folder created:", tmpdir)
    shutil.copy("file.txt", tmpdir)
```

---

### 8. **Finding Executable Files**

#### `shutil.which(command)`

* Returns the full path of an executable (like the Linux `which` command).

```python
print(shutil.which("python"))
# Output: C:\Python39\python.exe  (Windows) or /usr/bin/python3 (Linux)
```

---

### 9. **Error Handling**

All `shutil` operations can raise exceptions:

* `FileNotFoundError` – Source doesn’t exist
* `PermissionError` – Insufficient permissions
* `shutil.Error` – Copy/move-related error

Example:

```python
try:
    shutil.copy("file1.txt", "dir/")
except shutil.Error as e:
    print("Error:", e)
```

---

## ⚙️ Practical DevOps / Automation Use Cases

| Task                        | `shutil` Function | Example                                             |
| --------------------------- | ----------------- | --------------------------------------------------- |
| Backup configuration files  | `copy2()`         | `shutil.copy2("/etc/nginx/nginx.conf", "/backup/")` |
| Move logs to archive        | `move()`          | `shutil.move("/var/log/app.log", "/archive/")`      |
| Clean temporary build files | `rmtree()`        | `shutil.rmtree("/tmp/build")`                       |
| Package deployment folder   | `make_archive()`  | `shutil.make_archive("deploy", "zip", "app/")`      |
| Verify space before backup  | `disk_usage()`    | check free space on `/`                             |

---

## 🧠 Interview Questions on `shutil`

1. **What is the difference between `shutil.copy()` and `shutil.copy2()`?**
   → `copy2()` preserves metadata; `copy()` does not.

2. **How do you copy an entire directory tree?**
   → Use `shutil.copytree(src, dst)`.

3. **Which function deletes a directory tree recursively?**
   → `shutil.rmtree(path)`.

4. **How to create and extract a `.zip` file in Python?**
   → Use `make_archive()` and `unpack_archive()`.

5. **How to find where a command (like `python`) is installed?**
   → `shutil.which("python")`.

6. **Can `shutil.move()` rename files?**
   → Yes, if destination path has a different filename.

7. **What’s the safest way to copy directories while ignoring some files?**
   → Use `copytree()` with `ignore_patterns()`.

---

## ✅ Summary

| Operation        | Function             | Equivalent Linux Command |
| ---------------- | -------------------- | ------------------------ |
| Copy file        | `copy()` / `copy2()` | `cp`                     |
| Copy directory   | `copytree()`         | `cp -r`                  |
| Move / rename    | `move()`             | `mv`                     |
| Delete directory | `rmtree()`           | `rm -rf`                 |
| Archive folder   | `make_archive()`     | `zip` / `tar`            |
| Extract archive  | `unpack_archive()`   | `unzip` / `tar -x`       |
| Disk usage info  | `disk_usage()`       | `df -h`                  |
| Find binary path | `which()`            | `which`                  |

---

Would you like me to create a **ready-to-download PDF notes version** of this `shutil` guide (for study or interview use)?
