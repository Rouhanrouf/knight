# knight
KNIGHT — Autonomous reconnaissance, vulnerability assessment, and controlled offensive security framework for authorized penetration testing and security research.
# ⚔️ KNIGHT

### Autonomous Reconnaissance, Vulnerability Assessment & Controlled Offensive Security Framework

**KNIGHT** is a modular Python-based security assessment framework designed for authorized penetration testing, vulnerability research, CTF environments, and security laboratories.

It combines reconnaissance, attack-surface discovery, vulnerability assessment, controlled offensive testing, evidence collection, analysis, and automated reporting into a unified workflow.

> **Recon. Discover. Assess. Validate. Report.**

---

## ✨ Features

### 🔎 Reconnaissance

KNIGHT automates the initial attack-surface discovery process.

- Subdomain enumeration
- DNS reconnaissance
- Certificate Transparency discovery
- Live host detection
- HTTP/HTTPS service identification
- Scope-aware host filtering

---

### 🌐 Web Discovery

KNIGHT builds an attack-surface map from discovered web applications.

- Automated web crawling
- Endpoint discovery
- Historical URL discovery
- Parameter discovery
- JavaScript resource discovery
- JavaScript secret/token detection
- Redirect-aware crawling
- Scope-aware URL filtering

Supported discovery tooling can include:

- `subfinder`
- `gau`
- `waybackurls`

---

## 🛡️ Vulnerability Assessment

KNIGHT includes automated checks for common web application security issues.

### Supported assessment areas

- Reflected XSS
- SQL injection indicators
- Open redirects
- IDOR analysis
- Information disclosure
- JavaScript secrets
- Security misconfigurations
- Nuclei-based vulnerability detection

Findings are normalized and classified before appearing in the final report.

---

# ⚔️ Offensive Security Mode

KNIGHT also contains a dedicated **controlled offensive-testing layer** for authorized assessments and laboratory environments.

When enabled, the framework can perform additional security-testing workflows against findings that meet the framework's validation requirements.

### Offensive capabilities include

- Controlled SQL injection testing
- XSS testing workflows
- Authentication-bypass testing
- LFI/RFI testing
- Command-injection testing
- Credential-testing workflows
- Exploit/payload generation
- XSS callback/capture functionality for controlled environments
- Evidence collection from offensive testing

Offensive functionality is separated from the standard assessment pipeline so normal reconnaissance and vulnerability assessment can be performed without automatically enabling these modules.

---

# 🧠 Analysis Engine

KNIGHT does more than simply collect scanner output.

The analysis layer provides:

- Finding normalization
- Duplicate removal
- Confidence classification
- Finding-status classification
- Signature-based triage
- Correlation of results from multiple scanners
- AI-assisted finding analysis
- Evidence correlation

The framework distinguishes between potential findings and findings that have sufficient evidence for a higher confidence classification.

---

# 📝 Automated Reporting

After the assessment, KNIGHT generates a structured security report containing information such as:

- Target information
- Scope
- Scan statistics
- Discovered hosts
- Discovered URLs
- Parameters
- Vulnerability findings
- Confidence/status
- Evidence
- Reproduction information
- Analysis
- Recommendations

Reports and evidence are stored locally for later review.

---

# 🏗️ Architecture

```text
                         ┌─────────────────┐
                         │     KNIGHT      │
                         └────────┬────────┘
                                  │
                     ┌────────────▼────────────┐
                     │ Authorization & Scope   │
                     └────────────┬────────────┘
                                  │
                     ┌────────────▼────────────┐
                     │     RECONNAISSANCE      │
                     │                         │
                     │ DNS / CT / Subdomains   │
                     │ Live Host Detection     │
                     └────────────┬────────────┘
                                  │
                     ┌────────────▼────────────┐
                     │    WEB DISCOVERY        │
                     │                         │
                     │ Crawl / URLs / Params   │
                     │ JavaScript Discovery    │
                     └────────────┬────────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
              ▼                   ▼                   ▼
        ┌───────────┐       ┌───────────┐       ┌───────────┐
        │    XSS    │       │   SQLi    │       │   IDOR    │
        └─────┬─────┘       └─────┬─────┘       └─────┬─────┘
              │                   │                   │
              └───────────────────┼───────────────────┘
                                  │
                     ┌────────────▼────────────┐
                     │   NUCLEI / ASSESSMENT   │
                     └────────────┬────────────┘
                                  │
                         ┌────────▼────────┐
                         │    OFFENSIVE     │
                         │      MODE        │
                         └────────┬─────────┘
                                  │
                     ┌────────────▼────────────┐
                     │    ANALYSIS / TRIAGE    │
                     └────────────┬────────────┘
                                  │
                     ┌────────────▼────────────┐
                     │    EVIDENCE / REPORT    │
                     └─────────────────────────┘
KNIGHT is designed around explicit authorization.

Before scanning a target, the operator must confirm that they have permission to perform the assessment.

Scope can also be defined using a scope file.

Example:

example.com
*.example.com
!admin.example.com

This allows the operator to define which hosts are included and which are excluded.

Important

KNIGHT should only be used against:

Systems you own
Systems where you have written authorization
Dedicated penetration-testing environments
CTFs
Local security laboratories
Other explicitly authorized targets

Do not use KNIGHT to scan or attack systems without permission.

⚙️ Installation
Requirements

Python 3.10+ is recommended.

Clone the repository:

git clone https://github.com/YOUR_USERNAME/KNIGHT.git
cd KNIGHT

Create a virtual environment:

python3 -m venv .venv

Activate it on macOS/Linux:

source .venv/bin/activate

Windows:

.venv\Scripts\activate

Install Python dependencies:

pip install -r requirements.txt
🔧 External Tools

Depending on the features you use, KNIGHT can integrate with external security tools such as:

subfinder
gau
waybackurls
nuclei

Make sure each tool is installed and available in your system PATH.

Verify:

subfinder -version
gau -version
nuclei -version
🚀 Usage

Basic scan:

python3 knight.py example.com

Explicit HTTPS target:

python3 knight.py https://example.com

Turbo mode:

python3 knight.py example.com --turbo

Use a custom scope:

python3 knight.py example.com --scope-file scope.txt

Skip injection testing:

python3 knight.py example.com --skip-injection

Skip JavaScript secret analysis:

python3 knight.py example.com --skip-js-secrets
⚔️ Offensive Mode

Offensive functionality is explicitly separated from the standard assessment workflow.

For an authorized laboratory or penetration test:

python3 knight.py TARGET --offensive

Use offensive functionality only when the target is explicitly authorized.

🧪 Laboratory Usage

KNIGHT can be used with intentionally vulnerable applications and local security laboratories.

Example:

http://127.0.0.1:8787

A local lab makes it possible to safely test:

XSS detection
Redirect detection
Information disclosure detection
SQL injection indicators
Crawling
Evidence collection
Reporting
Offensive testing workflows

A dedicated laboratory is recommended when developing or modifying KNIGHT's offensive modules.

📂 Project Structure

A typical KNIGHT installation contains:

KNIGHT/
│
├── knight.py
├── requirements.txt
├── README.md
│
├── evidence/
│   └── ...
│
├── logs/
│   └── ...
│
├── vuln_db.json
└── scope_confirmations.log
📊 Assessment Pipeline
Target
  │
  ▼
Authorization
  │
  ▼
Scope Validation
  │
  ▼
Recon
  │
  ▼
Live Host Detection
  │
  ▼
URL Discovery
  │
  ▼
Crawler
  │
  ▼
Parameter Discovery
  │
  ▼
JavaScript Analysis
  │
  ▼
Vulnerability Assessment
  │
  ├── XSS
  ├── SQLi
  ├── IDOR
  ├── Open Redirect
  ├── Information Disclosure
  └── Nuclei
  │
  ▼
Optional Offensive Testing
  │
  ▼
Finding Triage
  │
  ▼
Evidence Collection
  │
  ▼
Report
🎯 Design Goals

KNIGHT is designed around five principles:

1. Automation

Reduce repetitive manual work during security assessments.

2. Correlation

Combine information from multiple discovery and assessment sources.

3. Validation

Separate potential indicators from higher-confidence findings.

4. Scope Awareness

Keep scanning tied to explicitly authorized targets and defined scope.

5. Reproducibility

Preserve evidence and assessment information so findings can be reviewed later.

🧩 Technology Stack

KNIGHT is primarily built with:

Python
HTTPX
Playwright
BeautifulSoup
Requests-compatible HTTP workflows
Nuclei
Subfinder
GAU
Wayback URL discovery
ReportLab

Additional tools may be used depending on the enabled modules.

📜 Disclaimer

KNIGHT is a security research and penetration-testing framework.

The author does not encourage or support unauthorized:

Scanning
Exploitation
Credential attacks
Data extraction
Session abuse
Access to systems belonging to other individuals or organizations

You are responsible for ensuring that you have appropriate authorization before using KNIGHT against a target.

Use it responsibly.

🛠️ Roadmap

Future development may include:

 Improved attack-surface visualization
 Better endpoint fingerprinting
 Enhanced vulnerability correlation
 Plugin architecture
 More report formats
 Improved false-positive reduction
 Web-based assessment dashboard
 Distributed scanning
 Improved laboratory tooling
 Additional security-testing integrations
🤝 Contributing

Contributions are welcome.

If you want to contribute:

Fork the repository.
Create a feature branch.
git checkout -b feature/my-feature
Make your changes.
Test them against an authorized laboratory.
Submit a pull request.

Please avoid submitting changes that remove authorization or scope protections.

⭐ Support

If KNIGHT is useful for your security research, consider starring the repository.

⚔️ KNIGHT
Recon. Discover. Assess. Validate. Report.
