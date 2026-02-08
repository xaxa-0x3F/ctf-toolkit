# 🦠 Reverse Engineering & Malware

## 🧬 Static Analysis

### Basic Inspection
* **Strings:** `strings binary` (Find hardcoded passwords/URLs).
* **Symbol Table:** `nm binary` (List functions).
* **Libraries:** `ldd binary` (See linked libraries).

### Specialized File Types
* **Oracle Forms:** (`.pll` / `.plx` / `.pld`) - Use `strings` or search for an Oracle Decompiler.

### Decompilers & Disassemblers
| Tool | Usage |
| :--- | :--- |
| **Ghidra** | NSA's free decompiler. Best free GUI for seeing C code from ASM. |
| **IDA Free** | Industry standard disassembler. |
| **Cutter** | GUI for Rizin/Radare2. Great for quick analysis. |
| **Dogbolt** | [Dogbolt.org](https://dogbolt.org/) (Online Decompiler explorer). |

---

## 🧩 Malware Analysis Tools
| Tool | Link | Purpose |
| :--- | :--- | :--- |
| **VirusTotal** | [Website](https://www.virustotal.com) | Upload file to scan against AV engines. |
| **ProcMon** | [Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon) | Monitor Windows process/registry activity in real-time. |
| **Any.Run** | [Website](https://any.run/) | Interactive online malware sandbox. |
| **ImHex** | [GitHub](https://github.com/WerWolv/ImHex) | Modern Hex Editor for pattern matching. |