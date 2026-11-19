# Project 14: Build a Threat Actor Profile from Public Reporting

**Level:** Beginner | **Track:** Threat Intelligence & Threat Hunting

## Objective
Complete a repeatable defensive exercise focused on build a threat actor profile from public reporting. Produce traceable evidence, explain confidence and uncertainty, and translate observations into proportionate defensive improvements.

## Scope and authorization
Use public information in accordance with its terms, synthetic datasets, systems you own, or systems covered by explicit written authorization. Do not access third-party systems, collect credentials, target private individuals, or deploy malware. Keep testing read-only and isolated.

## Prerequisites
- Linux workstation or Kali; Windows event sources where relevant.
- Python 3.10+, Git, text editor, JSON/CSV viewer.
- Synthetic logs, benign indicators, and an evidence folder.
- Basic understanding of DNS, HTTP, authentication, and network telemetry.

## Lab setup
1. Create `data/raw`, `data/processed`, `src`, `evidence`, and `reports`.
2. Use clearly labeled synthetic records and reserved example domains/IPs.
3. Preserve raw input; record source, license, collection date, and SHA-256.
4. Create a Python virtual environment; install only required parsing libraries.
5. Write the investigation question and hypothesis before analysis.

## Walkthrough
1. **Frame the question:** State the defensive problem, scope, and what evidence could support or disprove the hypothesis.
2. **Collect:** Use approved public reporting, documentation, or synthetic lab data. Record publisher, URL, publication/access dates, and restrictions.
3. **Normalize:** Preserve original values and timestamps; validate types and flag malformed/conflicting records.
4. **Enrich:** Add relevant context with source attribution. Treat reputation matches as leads, not verdicts.
5. **Correlate and analyze:** Compare independent evidence, document alternative explanations, and map ATT&CK only where behavior is supported.
6. **Assess:** Score confidence, freshness, relevance, and potential impact separately.
7. **Report:** Summarize observations, methods, limitations, evidence references, and recommended defensive actions.
8. **Validate:** Replay against a second synthetic dataset and confirm repeatable, explainable results.

## Example workspace commands
```bash
mkdir -p data/{raw,processed} src evidence reports
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
find data/raw -type f -maxdepth 1 -print
sha256sum data/raw/* 2>/dev/null
```

For JSON input inspection:
```bash
python - <<'PY'
import json
from pathlib import Path
for p in Path("data/raw").glob("*.json"):
    obj=json.loads(p.read_text())
    print(p.name, "records:", len(obj) if isinstance(obj,list) else 1)
PY
```
Use read-only queries and synthetic data; do not scan or test assets outside the authorized scope.

## Expected output
- Reproducible collection/analysis notes and normalized data or query results.
- Evidence register with provenance, timestamps, confidence, and limitations.
- Analyst report with question, methodology, observations, assessment, and next steps.
- Three project-specific simulated training illustrations.

## Findings and risk assessment
For each observation capture an evidence ID, fact, source, first/last-seen time, confidence rationale, relevance, impact, and alternative explanation. Separate facts from hypotheses. Discuss false-positive and stale-data risks. An IOC match alone does not prove compromise.

## Framework mapping
Map supported behavior to MITRE ATT&CK tactics/techniques where applicable. Use CWE/OWASP only when the project genuinely concerns a weakness or application risk. Record framework version and mapping rationale; otherwise mark not applicable.

## Remediation
Recommend proportionate actions such as validating telemetry, tuning detections, reviewing indicators before blocking, improving logging, updating playbooks, and communicating uncertainty. Assign owner, priority, and target date.

## Validation criteria
- Inputs are traceable, checksummed, and labeled simulated or public-source.
- Workflow is repeatable and produces explainable results.
- Conclusions link to evidence and state confidence and limitations.
- Benign explanations and false positives are considered.
- Another analyst can reproduce the result and validate recommendations.

## Evidence and reporting checklist
- [ ] Scope, authorization, and hypothesis recorded
- [ ] Sources, dates, terms, and checksums documented
- [ ] Raw data preserved; transformations repeatable
- [ ] Findings linked to evidence and confidence rationale
- [ ] Framework mappings justified or marked N/A
- [ ] Recommendations and validation results documented

## Deliverables
Commit sanitized scripts, schema, synthetic samples, and report. Never commit secrets, personal data, customer telemetry, or restricted source content.

---
*All images in this folder are simulated training illustrations—not actual screenshots or evidence from a live investigation.*
