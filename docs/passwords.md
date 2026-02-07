# 🗝 Password Cracking & Wordlists

### 📂 Wordlists
[cite_start]*Any list I have used is marked with an asterisk (*)* [cite: 27, 28]

* **[RockYou*](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt):** Most popular wordlist. [cite_start]Always start here[cite: 29].
* [cite_start]**[CrackStation*](https://crackstation.net/):** Online MD5, Very Large, Pretty Popular[cite: 30].
* [cite_start]**[English Adjectives*](https://github.com/dwyl/english-words):** Useful for combinatory attacks[cite: 31].
* [cite_start]**[Crackstation (Rainbow)*](https://crackstation.net/):** Rainbow Table for hashes[cite: 32].
* [cite_start]**[Hashes.com*](https://hashes.com/en/decrypt/hash):** Rainbow Table for hashes[cite: 33].
* [cite_start]**[Weakpass](https://weakpass.com):** Huge collection of wordlists[cite: 39].

### 🔨 Cracking Tools
| Tool | Description | Usage Command |
| :--- | :--- | :--- |
| **Hashcat** | [cite_start]GPU Cracking (Fastest) [cite: 25] | `hashcat -m 0 hash.txt wordlist.txt` |
| **John the Ripper** | [cite_start]CPU Cracking (Versatile) [cite: 25] | `john --wordlist=rockyou.txt hash.txt` |
| **Ophcrack** | [cite_start]Windows Passwords [cite: 25] | Load ISO/Tables to crack Windows login. |
| **CrackStation** | [cite_start]Online Cracking [cite: 25] | Paste hash directly into website. |

### 📄 File Cracking (Preparation)
Before cracking a file, you need to turn it into a "hash" that John can read.
* [cite_start]**PDF Files:** `pdf2john file.pdf > hash.txt` [cite: 25]
* [cite_start]**Zip Files:** `zip2john file.zip > hash.txt` or `fCrackZip` [cite: 26]
* **Windows SAM:** `samdump2 SYSTEM SAM > hashes.txt`
