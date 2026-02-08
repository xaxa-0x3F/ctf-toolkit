# 🔎 Forensics & Log Analysis

*Blue team skills: finding the needle in the haystack.*

## 📜 Log Analysis

### Quick Filters (The "Top 10" Method)
Find the noisiest IP address in a log file (likely the attacker).

```bash
cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -10
```

### Status Code Hunting
* **200 (OK):** Success. Did they steal data?
* **404 (Not Found):** Scanning/Fuzzing.
* **500 (Server Error):** They broke something (SQLi attempts).

```bash
# Show only successful requests from a suspect IP
grep "192.168.1.5" access.log | grep " 200 "
```

### User-Agent Analysis
Attackers often use default tool agents (sqlmap, curl, python).
```bash
cat access.log | awk -F\" '{print $6}' | sort | uniq -c | sort -nr
```

---

## 📦 File Forensics

### File Types & Metadata
* **Check real type:** `file unknown_file`
* **Read metadata:** `exiftool unknown_file`
* **Hex Dump:** `xxd unknown_file | head`

### Strings
Extract readable text from binaries or memory dumps.
```bash
strings -n 6 binary.exe | less
# -n 6: Only show strings longer than 6 chars (reduces noise)
```

### Archives
| Command | Action |
| :--- | :--- |
| `tar -xvf file.tar` | Extract Tar. |
| `tar -xzvf file.tar.gz` | Extract Gzip Tar. |
| `unzip file.zip` | Extract Zip. |
| `binwalk -e file.bin` | Extract hidden files from firmware/binaries. |