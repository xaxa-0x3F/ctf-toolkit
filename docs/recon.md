# 📡 Reconnaissance & Enumeration

*The art of finding the target. If you can't find it, you can't hack it.*

!!! quote "Methodology"
    **1. Scope:** Identify your target IP or Domain.
    **2. Scan:** Find open ports and running services.
    **3. Enumerate:** Interrogate those services for versions, users, and shares.
    **4. OSINT:** Find public info (passive recon).

---

## 🐧 Network Scanning (Active)

### IP & Connectivity
Start by verifying your connection to the target/box.

| Command | Description |
| :--- | :--- |
| `ip a` | Show your IP address and interfaces (tun0 is usually VPN). |
| `ping -c 4 <ip>` | Test connectivity (stop after 4 pings). |
| `fping -a -g 192.168.1.0/24` | Ping sweep an entire subnet to find live hosts. |
| `arp-scan -l` | Scan local network (Layer 2) for devices. |

### Port Scanning
*Find the doors.*

=== "Nmap (Standard)"
    The gold standard. Reliable but can be slow.
    ```bash
    # Basic Safe Scan (Scripts + Versions)
    nmap -sC -sV -oA nmap_initial <target_ip>

    # All Ports (Thorough)
    nmap -p- -T4 <target_ip>

    # UDP Scan (Don't forget this!)
    sudo nmap -sU --top-ports 100 <target_ip>
    ```

=== "Rustscan (Fast)"
    Much faster than Nmap. Great for the initial "rush".
    ```bash
    # Scan all ports in seconds, then pipe to Nmap
    rustscan -a <target_ip> -- -sC -sV
    ```

=== "Masscan (Large Scale)"
    When you need to scan the entire internet (or a huge subnet).
    ```bash
    masscan -p1-65535 <target_ip> --rate=1000
    ```

---

## 🔬 Service Enumeration
*You found an open port. Now, what is it doing?*

### 📁 SMB (Windows Shares)
*Port 139 / 445*
Often contains sensitive files or credentials.

```bash
# List shares (Null Session)
smbclient -L //<target_ip> -N

# Connect to a share
smbclient //<target_ip>/sharename -N

# Linux Enum Tool (Runs everything)
enum4linux -a <target_ip>
```

### 📂 NFS (Linux Shares)
*Port 2049*
Network File Systems often have weak permissions.

```bash
# List available mounts
showmount -e <target_ip>

# Mount it to your machine
sudo mount -t nfs <target_ip>:/home/remote_folder /mnt/local_folder
```

### 🌐 DNS (Domain Names)
*Port 53*
Look for hidden subdomains or internal network info.

```bash
# Zone Transfer (Try to steal the whole map)
dig axfr @<target_ip> domain.com

# Reverse Lookup
dig -x <target_ip>
```

---

## 🕸️ Web Enumeration
*Finding hidden pages and subdomains.*

### Directory Brute-Forcing
*Finding `/admin`, `/login`, `/backup`.*

=== "Gobuster"
    ```bash
    gobuster dir -u http://<target_ip> -w /usr/share/wordlists/dirb/common.txt
    ```

=== "Feroxbuster"
    Recursive and fast (Written in Rust).
    ```bash
    feroxbuster -u http://<target_ip>
    ```

### Subdomain Enumeration
*Finding `dev.site.com` or `vpn.site.com`.*

```bash
# FFUF (Fuzz Faster U Fool)
ffuf -u [http://site.com](http://site.com) -H "Host: FUZZ.site.com" -w /usr/share/wordlists/subdomains.txt
```

### Tech Stack ID
*What are they running? (WordPress? Apache? PHP version?)*

* **Command Line:** `whatweb <url>`
* **Browser:** [Wappalyzer Extension](https://www.wappalyzer.com/)

---

## 🕵️ OSINT (Passive)
*Gathering info without touching the target.*

### 🗺️ Visual & Geolocation
| Tool | Link | Usage / Notes |
| :--- | :--- | :--- |
| **Reverse Image** | [Yandex](https://yandex.com/images/) / [Google](https://images.google.com) / [Duplicheck](https://www.duplichecker.com/reverse-image-search.php) | Upload images to find location/origin. Yandex is best for faces/Europe. |
| **Geolocation** | [Google Lens](https://lens.google.com/) / [What3Words](https://what3words.com/) | Identify landmarks from photos or convert 3-word addresses. |
| **Wifi Recon** | [Wigle](https://wigle.net/) / [Wifi Map](https://www.wifimap.io/) | Global map of Wifi SSIDs. Good for finding physical locations. |
| **Waypoints** | [OpenNav](https://opennav.com/) | Find marine and aviation waypoints. |

### 🌐 Domain & Network Info
| Tool | Link | Usage / Notes |
| :--- | :--- | :--- |
| **IP Info** | [XMyIP](https://xmyip.com/) / [WhoIs](https://who.is/) | Registration info, ISP, and ownership. |
| **Wayback Machine** | [Archive.org](https://web.archive.org/) | View deleted pages or old versions of a site. |
| **Google Dorks** | [Exploit-DB](https://www.exploit-db.com/google-hacking-database) | `site:target.com filetype:pdf "confidential"` |

### 👤 Identity & Documents
| Tool | Link | Usage / Notes |
| :--- | :--- | :--- |
| **Usernames** | [Sherlock](https://github.com/sherlock-project/sherlock) | `python3 sherlock.py user` (Check social media usage). |
| **Passport (MRZ)** | [GlobalPass](https://globalpass.ch/mrz-check/) / [Wiki Guide](https://en.wikipedia.org/wiki/Machine-readable_passport) | Decode the "Machine Readable Zone" on passports. |

### 🧩 Data Decoding
* **Decimal to IP:** Convert `2130706433` -> `127.0.0.1`. [Browserling](https://www.browserling.com/tools/dec-to-ip).
* **UUID Decoding:** Decode Universal Unique IDs. [UUID Tools](https://www.uuidtools.com/decode).
* **QR Codes:** Decode damaged/blurry codes. [QR Code Raptor](https://qrcoderaptor.com/) or [Inlite](https://online-barcode-reader.inlite.com/).
* **Exif Data:** Read image metadata using `exiftool image.jpg`.