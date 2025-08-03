

# 📘 Chapter 12: File Handling Like a Developer

> *"Your code’s memory fades when the program stops. Files are its diary — write it well."*

---

## 🎯 Chapter Goals

By the end of this chapter, readers will:

* Understand **how operating systems manage files** and why this matters for performance.
* Read, write, and modify **text, binary, and structured files**.
* Handle **large files** without exhausting memory.
* Master **safe file handling** using `with` blocks and temporary files.
* Manage **file paths**, create directories, and detect file existence.
* Handle **encodings** and prevent data corruption.
* Process **CSV** and tabular data like a pro.
* Build reusable **file-handling utilities** for automation.

---

## 📂 Chapter Structure

### 12.1 What Exactly is a File?

* OS-level file concepts: filename, inode, permissions.
* Difference between **text files** (character encoding) and **binary files** (raw bytes).
* Storage devices and how read/write speeds differ (SSD vs HDD).

📦 **Philosophy Box:**
*"Knowing how files work under the hood is like knowing the anatomy before becoming a surgeon."*

---

### 12.2 File Paths and Navigation

* Absolute vs relative paths.
* Platform differences (`/` vs `\`).
* Using `os`, `pathlib` for path safety.
* Detecting file existence before reading/writing.

🧪 Example:

```python
from pathlib import Path
p = Path("data/report.txt")
if p.exists():
    print("File found!")
```

---

### 12.3 Opening Files — Modes and Buffers

* Modes: `"r"`, `"w"`, `"a"`, `"rb"`, `"wb"`, `"x"`.
* Append vs overwrite behavior.
* `"x"` mode for fail-safe write (errors if file exists).
* Buffering parameter in `open()` for performance tuning.

---

### 12.4 Reading Files — Small and Large

* `.read()`, `.readline()`, `.readlines()`.
* Iterating over file object directly (memory safe).
* Reading in **chunks** for large files.

📦 **Performance Hack:**
Read 1MB chunks with `f.read(1024*1024)` when parsing huge logs.

---

### 12.5 Writing Files — Overwrite, Append, and Atomic Writes

* Writing strings and lists of strings.
* Appending logs without losing history.
* **Atomic write pattern** using temporary files to prevent data corruption.

---

### 12.6 Using `with` — The Professional Way

* Guarantees file closure.
* Exception safety.
* Nesting multiple `with` statements for working on multiple files.

---

### 12.7 Binary Files — Images, PDFs, and More

* Reading/writing bytes with `"rb"` / `"wb"`.
* Copying binary files.
* Reading binary headers for format detection.

---

### 12.8 Encodings and Unicode Safety

* UTF-8 as the safest default.
* Reading files with unknown encoding (`errors="ignore"`).
* When to use `"latin-1"` or `"utf-16"`.

---

### 12.9 Buffering, Streaming, and Real-Time Processing

* Disabling buffering for real-time log monitoring.
* Streaming large files over the network without full memory load.

🧪 Example:

```python
import sys
with open("log.txt", "r") as f:
    for line in f:
        sys.stdout.write(line)
```

---

### 12.10 Working with CSV and Tabular Data

* Using `csv.reader` and `csv.writer`.
* `DictReader` and `DictWriter` for readable column-based access.
* Handling custom delimiters (`delimiter=";"`).

---

### 12.11 JSON and Config Files (Beyond CSV)

* `json.load()` and `json.dump()` for structured data.
* Pretty-printing JSON for human-readable storage.

---

### 12.12 File Metadata and Permissions

* Getting file size, modification time (`os.stat`).
* Checking read/write access (`os.access`).
* Changing file permissions (`os.chmod`).

---

### 12.13 Organizing and Managing Files

* Listing directory contents (`os.listdir`, `Path.iterdir`).
* Moving, copying, and deleting files with `shutil`.
* Creating directory trees safely.

---

### 12.14 Common File Handling Pitfalls

* Forgetting to close files (and how it leaks resources).
* Hardcoding paths (use `pathlib`).
* Ignoring encoding → mojibake (garbled text).
* Reading entire 10GB file into RAM.

---

### 12.15 Building File Utility Functions

* `read_file_lines(filename)` → returns list of lines safely.
* `append_to_log(logfile, message)` → writes with timestamp.
* `safe_copy(src, dst)` → with error handling.

---

## 📦 Bonus Boxes

* 📌 *Tech Tip:* Using `tempfile` for secure temporary file creation.
* 🧪 *Mini Lab:* Build a log rotation script that archives yesterday’s logs.
* ⚙️ *Under the Hood:* File descriptors, system calls, and why `with` closes them.

---

## 🧠 Concept Recall

* How does `"x"` mode differ from `"w"`?
* Why is reading in chunks better for huge files?
* How can you avoid data loss when writing to a file?
* What is the safest encoding to use for text files?

---

## ✅ Mastery Checklist

* [ ] I can open files in all modes and know their effects.
* [ ] I can process 1GB+ files without memory overflow.
* [ ] I can handle CSV, JSON, and binary files.
* [ ] I can create reusable file utility functions.

---

## 🧾 Cheatsheet (Chapter 12)

```python
# Read text file
with open("file.txt", "r", encoding="utf-8") as f:
    print(f.read())

# Write with overwrite protection
with open("file.txt", "x") as f:
    f.write("Data")

# Read binary file
with open("image.png", "rb") as img:
    data = img.read()

# CSV Reading
import csv
with open("data.csv", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row)

# JSON Writing
import json
with open("config.json", "w") as f:
    json.dump({"debug": True}, f, indent=4)
```

---

## 🔗 Transition to Chapter 13 — Error Handling and Defensive Programming

With great file power comes great responsibility —
and a missing file or wrong permission can crash your script instantly.

In the next chapter, we’ll learn **how to catch and handle file-related errors** gracefully,
turning your programs into **failure-proof tools**.

---

