# Project 31: Hunt Cloud Identity and Access Anomalies

**Level:** Intermediate | **Track:** Threat Intelligence & Threat Hunting

## Objective
Complete a repeatable defensive exercise focused on hunt cloud identity and access anomalies. Produce traceable evidence, explain confidence and uncertainty, and turn observations into proportionate defensive improvements.

## Scope and authorization
Use public information in accordance with its terms, synthetic datasets, systems you own, or systems covered by explicit written authorization. Do not access third-party systems, collect credentials, target private individuals, or deploy malware. Keep testing read-only and isolated.

## Prerequisites
- Linux/Kali workstation; Windows event sources where relevant.
- Python 3.10+, Git, editor, JSON/CSV viewer.
- Synthetic logs, benign indicators, and an evidence folder.
- Basic DNS, HTTP, authentication, and network telemetry knowledge.

## Lab setup
1. Create `data/raw`, `data/processed`, `src`, `evidence`, and `reports`.
2. Use labeled synthetic records, reserved example IP ranges, and example domains.
3. Preserve raw input; record source, license, collection date, and SHA-256.
4. Create a virtual environment and install only required parsing libraries.
5. Write the investigation question and hypothesis before analysis.

## Walkthrough
1. Frame the defensive question, scope, and evidence that could support or disprove the hypothesis.
2. Collect approved public reporting, documentation, or synthetic data; record publisher, URL, dates, and restrictions.
3. Normalize fields while preserving original values, timestamps, and malformed-record details.
4. Enrich with attributed context; reputation matches are leads, not verdicts.
5. Correlate independent evidence, document benign explanations, and map ATT&CK only when supported.
6. Assess confidence, freshness, relevance, and potential impact separately.
7. Report observations, methods, limitations, evidence references, and defensive actions.
8. Replay on a second synthetic dataset and verify repeatable, explainable results.

## Example commands
```bash
mkdir -p data/{raw,processed} src evidence reports
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
find data/raw -maxdepth 1 -type f -print
sha256sum data/raw/* 2>/dev/null
```
Inspect JSON safely:
```bash
python - <<'PY'
import json
from pathlib import Path
for p in Path("data/raw").glob("*.json"):
    x=json.loads(p.read_text())
    print(p.name, len(x) if isinstance(x,list) else 1)
PY
```
Use read-only queries and synthetic inputs; never scan or test assets outside the authorized scope.

## Expected output
- Reproducible collection/analysis notes and normalized data or query results.
- Evidence register with provenance, timestamps, confidence, and limitations.
- Analyst report with question, method, observations, assessment, and next steps.
- Three project-specific simulated SVG illustrations.

## Findings and risk assessment
Record evidence ID, observed fact, source, first/last-seen time, confidence rationale, relevance, impact, and alternative explanation. Separate facts from hypotheses. Discuss false positives and stale-data risks. An IOC match alone does not prove compromise.

## Framework mapping
Map supported behavior to MITRE ATT&CK where applicable. Use CWE/OWASP only when relevant; record framework version and mapping rationale or mark not applicable.

## Remediation
Recommend proportionate actions: validate telemetry, tune detections, review indicators before blocking, improve logging, update playbooks, and communicate uncertainty. Assign owner, priority, and target date.

## Validation criteria
- Inputs traceable, checksummed, and labeled as simulated or public-source.
- Workflow repeatable and outputs explainable.
- Conclusions link to evidence and state confidence/limitations.
- Benign explanations and false positives considered.
- A second analyst can reproduce and validate the recommendations.

## Evidence and reporting checklist
- [ ] Scope, authorization, and hypothesis recorded
- [ ] Sources, dates, terms, and checksums documented
- [ ] Raw data preserved; transformations repeatable
- [ ] Findings linked to evidence and confidence rationale
- [ ] Framework mappings justified or N/A
- [ ] Recommendations and validation documented

## Deliverables
Commit sanitized scripts, schema, synthetic samples, and report. Never commit secrets, personal data, customer telemetry, or restricted content.

---
*All diagrams are simulated training illustrations—not actual screenshots or live investigation evidence.*
