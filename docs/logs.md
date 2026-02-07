# 📜 Log Analysis

*A guide to finding the needle in the haystack. In CTFs, logs are usually massive text files containing evidence of an attack.*

### 🧰 The Toolkit
| Tool | Best For | Link |
| :--- | :--- | :--- |
| **Linux CLI** | The fastest way to parse massive files (`grep`, `awk`, `cut`). | Built-in |
| **Excel / Sheets** | Visual sorting by IP, Time, or Status Code. | N/A |
| **lnav** | An advanced log file navigator for the terminal with syntax highlighting. | [lnav.org](https://lnav.org/) |
| **CyberChef** | Decoding base64/hex strings found inside logs. | [CyberChef](https://gchq.github.io/CyberChef/) |
| **Drone Logs** | Specific tools for DJI/Flight data. | [AirData](https://app.airdata.com/) |

---

### 🧠 CLI Analysis Workflow
*Don't read lines one by one. Filter the noise.*

#### 1. The "Top 10" Method
Find out who is making the most noise. The IP with thousands of hits is usually the attacker running a scan.

    cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -10

#### 2. Filter by Status Code
* **200 (OK):** The attacker successfully loaded a page or stole a file.
* **404 (Not Found):** The attacker is guessing file names (scanning).
* **500 (Server Error):** The attacker broke something (likely SQL Injection).

    # Show me only successful requests from a specific bad IP
    grep "192.168.1.5" access.log | grep " 200 "

#### 3. User-Agent Hunting
Attackers often forget to change their tool's signature. Look for non-browser agents.

    # Show unique User-Agents
    cat access.log | awk -F\" '{print $6}' | sort | uniq -c | sort -nr

*Look for:* `sqlmap`, `nikto`, `gobuster`, `python-requests`, `curl`.

---

### 🚩 Common Attack Patterns
*What to `grep` for when looking for specific hacks.*

| Attack Type | Pattern to Search | Example Log Entry |
| :--- | :--- | :--- |
| **SQL Injection** | `UNION`, `SELECT`, `' OR 1=1`, `%27` | `index.php?id=1' UNION SELECT user,pass--` |
| **XSS** | `<script>`, `alert(`, `onerror=`, `%3Cscript%3E` | `search.php?q=<script>alert(1)</script>` |
| **Directory Traversal** | `../`, `..%2f`, `/etc/passwd`, `boot.ini` | `download.php?file=../../../../etc/passwd` |
| **Command Injection** | `;`, `|`, `&&`, `$(`, `whoami` | `ping.php?ip=8.8.8.8; whoami` |
| **Web Shells** | `cmd=`, `exec=`, `system=`, `eval` | `shell.php?cmd=ls` |

---

### 💡 Pro Tips
1.  **Decode on the fly:** If you see `%20` or `%27`, that is URL encoding. Use CyberChef to decode it to see the real attack.
2.  **Timeline is key:** Once you find the *first* successful attack (a 200 OK on a malicious payload), look at everything that happened *after* that second.
3.  **Exclude the noise:** If `index.php` is cluttering your view, remove it: `grep -v "index.php" access.log`.
