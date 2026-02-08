# 🗝 Password Cracking & Wordlists

## 📂 Wordlists
*Any list I have used is marked with an asterisk (*)*

| Wordlist | Description | Link / Download |
| :--- | :--- | :--- |
| **RockYou\*** | Most popular wordlist. Always start here. | [Download (GitHub)](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) |
| **CrackStation\*** | Online MD5, Very Large, Pretty Popular. | [Visit Site](https://crackstation.net/) |
| **English Adjectives\*** | Useful for combinatory attacks. | [View on GitHub](https://github.com/dwyl/english-words) |
| **Hashes.com\*** | Rainbow Table for hashes. | [Visit Site](https://hashes.com/en/decrypt/hash) |
| **Weakpass** | Huge collection of wordlists. | [Visit Site](https://weakpass.com) |

## 🔨 Cracking Tools

| Tool | Description | Install Command / Usage |
| :--- | :--- | :--- |
| **Hashcat** | GPU Cracking (Fastest) | `apt install hashcat`<br>`hashcat -m 0 hash.txt wordlist.txt` |
| **John the Ripper** | CPU Cracking (Versatile) | `apt install john`<br>`john --wordlist=rockyou.txt hash.txt` |
| **Ophcrack** | Windows Passwords | [Download ISO](https://ophcrack.sourceforge.io/)<br>Load tables to crack Windows login. |
| **CrackStation** | Online Cracking | [Go to Site](https://crackstation.net/)<br>Paste hash directly into website. |

## 📄 File Cracking (Preparation)
Before cracking a file, you need to turn it into a "hash" that John can read.

=== "PDF Files"
    Use `pdf2john` to extract the hash.
    ```bash
    # Install: usually comes with John
    pdf2john file.pdf > hash.txt
    ```

=== "Zip Files"
    Use `zip2john` or `fCrackZip`.
    ```bash
    zip2john file.zip > hash.txt
    # OR
    apt install fcrackzip
    ```

=== "Windows SAM"
    Dump the SAM database.
    ```bash
    # Requires samdump2
    apt install samdump2
    samdump2 SYSTEM SAM > hashes.txt
    ```
