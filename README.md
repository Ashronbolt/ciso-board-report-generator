CISO Board Report Generator
> Translates technical security findings into executive-level board reports — with financial exposure estimates, regulatory context, and sector-specific business impact analysis. Powered by Anthropic Claude AI.
---
The Problem This Solves:
Security teams speak in CVEs, misconfiguration IDs, and technical controls. Boards speak in £, risk appetite, and regulatory exposure.
This tool bridges that gap — taking raw technical findings and producing a board-ready report that a CEO or CFO can act on, without needing to understand the underlying technology.
---
What It Does
Takes security findings as input (demo data included — swap for real findings)
Calculates financial exposure estimates (breach cost, GDPR fines, downtime)
Applies sector-specific regulatory context
Uses Claude AI to generate a plain-English executive narrative
Outputs a complete board report with priority actions and ROI analysis
---
Sectors Supported:
Sector	Regulators	Frameworks
Financial Services	FCA, PRA, ICO	FCA SYSC, DORA, PCI-DSS, GDPR
Healthcare	ICO, CQC, NHS Digital	GDPR, DSP Toolkit, Cyber Essentials Plus
Critical Infrastructure	NCSC, Ofgem, ICO	NIS2 Directive, CAF, GDPR
Generic	ICO, NCSC	GDPR, Cyber Essentials, ISO 27001
---
Skills Demonstrated:
Area	Detail:
AI / LLM Integration	Anthropic Claude API, executive-level prompt engineering
Business Acumen	Financial exposure modelling, unit economics, ROI analysis
Cyber Risk Quantification	GDPR fine estimation, breach cost modelling, revenue at risk
Regulatory Knowledge	FCA, DORA, NIS2, GDPR, PCI-DSS, DSP Toolkit
Leadership Communication	Board-level narrative, plain English translation of technical risk
Python	Financial calculations, API integration, markdown report generation
---
Quick Start
1. Clone the repo
```bash
git clone https://github.com/YOUR-USERNAME/ciso-board-report-generator
cd ciso-board-report-generator
```
2. Install dependencies
```bash
pip install -r requirements.txt
```
3. Set your Anthropic API key
```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```
4. Run with demo data
```bash
python main.py
```
5. Use your own findings
Edit the `DEMO_FINDINGS` dictionary in `main.py` with your real assessment data:
```python
DEMO_FINDINGS = {
    "organisation": "Your Company Name",
    "sector": "Financial Services",  # or Healthcare, Critical Infrastructure, Generic
    "annual_revenue_gbp": 10000000,
    "employee_count": 150,
    "findings": [
        {
            "id": "F-001",
            "severity": "Critical",
            "category": "IAM",
            "title": "Your finding title",
            "detail": "Your finding detail",
            "affected_systems": ["system-name"]
        }
    ]
}
```
---
Example Output
```
========================================
  CISO BOARD REPORT — SUMMARY
========================================
Risk Rating    : Critical
Total Exposure : £8,243,000
Remediation    : £97,000
Revenue at Risk: 18.3%
----------------------------------------
Key Messages:
  • Customer data containing ~85,000 records is publicly accessible — live breach risk
  • Worst-case exposure of £8.2M vs £97K remediation cost — 84:1 ROI on fixing
  • Three Critical findings exploitable with no specialist skills
========================================
```
 See a full sample board report here
---
Financial Exposure Model
The tool calculates four exposure components automatically:
```
GDPR Fine = min(revenue × 4%, £17.5M) × sector_multiplier
Breach Cost = exposed_records × cost_per_record (sector-adjusted)
Downtime Cost = daily_revenue × estimated_downtime_days
Remediation Cost = (critical × £15K) + (high × £8K) + (medium × £3K)
```
Sector multipliers reflect real-world regulatory enforcement patterns — Financial Services carries a higher multiplier than Generic due to FCA/PRA enforcement history.
---
How It Works
```
Security Findings Input (DEMO_FINDINGS or real data)
        ↓
Financial Exposure Calculation (Python — no AI needed)
        ↓
Sector Context Applied (regulators, frameworks, risk profile)
        ↓
Prompt Engineering → Claude API
        ↓
Executive Narrative Generated (plain English, board-appropriate)
        ↓
Full Board Report — Markdown output with financials + priority actions
```
---
Design Decisions:
Why separate financial calculation from AI generation?
The financial exposure numbers are calculated deterministically in Python — not by the AI. This means the numbers are consistent and auditable. Claude is used only for narrative generation, where its language capability adds value.
Why JSON output from the AI?
Forcing structured JSON from Claude ensures the report sections are reliable and parseable — the tool doesn't depend on Claude formatting prose correctly every time.
Why sector-specific context?
A GDPR breach in Financial Services carries different regulatory consequences to the same breach in retail. The sector context ensures the regulatory narrative and financial estimates reflect real-world enforcement patterns.
---
Connecting to the Cloud Scanner
This tool is designed to accept output from the AWS Cloud Misconfiguration Scanner. Replace `DEMO_FINDINGS` with parsed output from that tool to create an end-to-end pipeline:
```
Cloud Scanner → Findings JSON → Board Report Generator → Executive Report
```
---
Project Structure
```
ciso-board-report-generator/
├── main.py                  # Core tool
├── requirements.txt         # Dependencies
├── .gitignore               # Excludes API keys
├── sample_output/
│   └── board_report.md      # Example board report
└── README.md
```
---
Author: Ashish Mukherjee

---
Disclaimer
Financial exposure estimates are indicative only and based on industry benchmarks. They should not be used as the sole basis for regulatory reporting or board decision-making without review by a qualified professional.
