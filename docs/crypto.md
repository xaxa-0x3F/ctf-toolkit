# 🔐 Cryptography & Steganography

## 🕵️ Cipher Identification
Before cracking, identify the cipher.

1.  **[Cipher Identifier (dCode)](https://www.dcode.fr/cipher-identifier)** - Best general purpose identifier.
2.  **[Boxentriq](https://www.boxentriq.com/code-breaking/cipher-identifier)** - Good for puzzle ciphers.
3.  **[CyberChef](https://gchq.github.io/CyberChef/)** - Use the "Magic" wand feature.

## 🛠️ Decryption Tools

| Algorithm | Tool/Link | Notes |
| :--- | :--- | :--- |
| **Base64** | `echo "text" \| base64 -d` | Ends with `=` usually. |
| **Hex** | [CyberChef (From Hex)](https://gchq.github.io/CyberChef/) | Looks like `48 65 6c 6c 6f`. |
| **ASCII** | [Online ASCII Tools](https://onlineasciitools.com/) | Convert Hex, Decimal, and Binary to text. |
| **Rot13/Caesar** | [Rot13.com](https://rot13.com/) | Simple letter shifting. |
| **RSA** | [RsaCtfTool](https://github.com/RsaCtfTool/RsaCtfTool) | Recover private keys from weak public keys. |
| **AES** | [Devglan](https://www.devglan.com/online-tools/aes-encryption-decryption) | Online AES decryptor (Needs Key/IV). |

---

## 🖼️ Steganography
*Hiding data inside images and audio.*

### Image Analysis
| Tool | Link | Best For |
| :--- | :--- | :--- |
| **Aperi'Solve** | [Aperi'Solve](https://www.aperisolve.com/) | **All-in-one.** Runs zsteg, steghide, exiftool automatically. |
| **StegOnline** | [StegOnline](https://stegonline.georgeom.net/) | Visual bit plane analysis. |
| **ExifTool** | `exiftool image.jpg` | Reading metadata (GPS, Author, Comments). |
| **ZSteg** | `zsteg -a image.png` | Finding LSB data in PNGs. |
| **Steghide** | `steghide extract -sf image.jpg` | Extracting password-protected hidden files. |

### Audio & Misc
* **Spectrograms:** Open audio in [Audacity](https://www.audacityteam.org/) and view "Spectrogram" to see hidden text.
* **DTMF Tones:** Decode phone dial tones with [RIBT Decoder](https://ribt.net/dtmf/).