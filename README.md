# ⬡ SentinelAI — Malware Analysis Platform

**Professional malware analysis platform built for security researchers.**  
Designed to be presented at enterprise level (Google, etc.)

---

## Features

| Feature | Details |
|---|---|
| **File Support** | ALL types — .exe, .dll, .bat, .ps1, .vbs, .js, .py, .pdf, .doc, .ino, .apk, .zip, .rar, .7z, .tar, .gz + everything else |
| **Archive Extraction** | ZIP, RAR, 7z, TAR, GZ, BZ2 — recursive extraction, each file analyzed separately |
| **Static Analysis** | Hash (MD5/SHA1/SHA256/SHA512), entropy, strings, PE headers, OLE macros |
| **YARA Detection** | 12+ built-in rules: Ransomware, RAT, Keylogger, Rootkit, Trojan, Spyware, Worm, Cryptominer, Packer, Script, Network, Persistence |
| **PE Analysis** | Sections, imports, exports, suspicious API calls categorized with explanations |
| **OLE/Office Analysis** | VBA macro detection in .doc, .xls, .ppt files |
| **Risk Scoring** | 0–100 score with full breakdown: what is harmful, why, what it means |
| **PDF Reports** | Deep professional reports — suitable for Google security team review |
| **Dashboard** | Rich black & white UI, real-time stats, drag & drop, scan history |
| **Database** | SQLite (local file in `database/sentinel.db`) — no external DB needed |

---


## Project Structure

```
SentinelAI/
├── app.py                  ← Main server (run this)
├── analyzer.py             ← Core static analysis engine
├── report_generator.py     ← PDF report generator
├── database_handler.py     ← SQLite database
├── file_handler.py         ← Archive extraction & file routing
├── requirements.txt        ← Python dependencies
├── yara_rules/
│   └── malware.yar         ← 12 YARA detection rules
├── database/
│   └── sentinel.db         ← SQLite DB (auto-created)
├── uploads/                ← Temp upload storage
└── reports/                ← Generated PDF reports
```

---

## Analysis Capabilities

### Static Analysis
- **Hashes**: MD5, SHA1, SHA256, SHA512
- **Entropy**: Shannon entropy with interpretation (detects packing/encryption)
- **String Extraction**: ASCII + Unicode — URLs, IPs, emails, registry keys, file paths
- **Suspicious Patterns**: 18+ regex patterns for C2, credentials, obfuscation, etc.

### PE (Windows Executable) Analysis
- Machine architecture, subsystem, entry point
- Section analysis with per-section entropy
- Import table — 200+ dangerous API calls categorized into 10 categories
- Packer detection (UPX, MPRESS, etc.)

### YARA Rules (Built-in)
1. Ransomware Behavior
2. Keylogger Behavior
3. RAT (Remote Access Trojan)
4. Trojan Dropper
5. Spyware / Data Exfiltration
6. Rootkit Behavior
7. Suspicious Network Activity
8. Packer / Obfuscation
9. Suspicious Scripts (PowerShell attacks)
10. Registry Persistence
11. Cryptocurrency Miner
12. Worm Propagation

### OLE / Office Document Analysis
- VBA macro detection in Word/Excel/PowerPoint files
- Document metadata extraction (author, company, timestamps)

---

## PDF Report Contents

1. **Verdict banner** — MALICIOUS/SUSPICIOUS/PUP/LOW RISK/CLEAN
2. **Risk score** — visual meter + score breakdown with explanations
3. **File information** — name, size, type, magic bytes
4. **Cryptographic hashes** — all 4 hash types
5. **Entropy analysis** — value, level, full explanation
6. **YARA detections** — rule name, category, severity, what it means
7. **Suspicious string patterns** — what was found, why it's dangerous
8. **Extracted artifacts** — URLs, IPs, registry keys, file paths
9. **PE analysis** — sections, dangerous APIs with explanations per category
10. **OLE analysis** — macro detection with explanation
11. **Risk score breakdown** — every contributing factor listed
12. **Analyst recommendations** — step-by-step actions based on verdict

---

## Adding Custom YARA Rules

Edit `yara_rules/malware.yar` and add your rules in YARA syntax:

```yara
rule MyCustomRule {
    meta:
        description = "Detects my custom pattern"
        severity = "HIGH"
        category = "Custom"
    strings:
        $s1 = "suspicious_string" ascii
    condition:
        any of them
}
```

---

## VirusTotal Integration (Optional)

To add VirusTotal API scanning, open `analyzer.py` and add at the top:

```python
VT_API_KEY = "your_api_key_here"  # or leave empty
```

The platform works fully without an API key.

---

*SentinelAI — Built for professional malware analysis*
