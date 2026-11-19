# Project 04: IP Address Reputation and Context Enrichment

**Level:** Beginner  
**Track:** Threat Intelligence and Threat Hunting  
**Project type:** Defensive lab / portfolio exercise

## 1. Objective
Design and complete a repeatable exercise for **IP Address Reputation and Context Enrichment**. Demonstrate how to collect or inspect relevant security data, preserve provenance, evaluate confidence, document limitations, and turn observations into actionable defensive decisions.

## 2. Scope and authorization
Work only with public information collected in accordance with its terms, synthetic datasets, systems you own, or systems covered by explicit written authorization. Do not probe third-party infrastructure, access private accounts, collect credentials, or identify/target private individuals. Keep this exercise offline or within an isolated lab where possible.

## 3. Prerequisites
- Kali Linux or a current Linux workstation; Windows is optional for endpoint-log exercises.
- Python 3.10+ and a virtual environment; Git for version control.
- A text editor and spreadsheet/JSON viewer.
- Synthetic logs, benign sample indicators, and a local folder for evidence.
- Familiarity with DNS, HTTP, authentication logs, and basic networking.

## 4. Lab setup
1. Create a dedicated project folder with `data/raw`, `data/processed`, `evidence`, `reports`, and `src` directories.
2. Use synthetic example records (RFC 5737 documentation IP ranges, reserved example domains, and clearly fake hashes). Label every generated record as simulated.
3. Record the dataset source, collection timestamp, license/terms, transformation steps, and SHA-256 checksum for each input file.
4. Create a Python virtual environment and install only the libraries needed for parsing and analysis (for example, `requests`, `pandas`, and `stix2` when relevant).
5. Define a written question or hypothesis before analysis; keep raw inputs immutable.

## 5. Workflow
1. **Define the question:** State what you need to learn, why it matters to defenders, and what would count as supporting or contradicting evidence.
2. **Collect safely:** Use approved public documentation, published threat reports, or supplied synthetic lab data. Capture source URL/title, publisher, publication date, access date, and any usage restrictions.
3. **Normalize:** Convert records into a consistent schema; preserve original values and timestamps. Do not silently discard malformed or conflicting records.
4. **Enrich and correlate:** Add only relevant context. Track which source supports each attribute and avoid treating a single reputation result as a verdict.
5. **Analyze:** Compare observations against the hypothesis. Map behavior to MITRE ATT&CK only when the behavior is supported by evidence; record alternative explanations.
6. **Prioritize:** Assess confidence, relevance, freshness, potential impact, and operational urgency separately.
7. **Document:** Produce a concise analyst summary, methods, evidence references, limitations, and recommended defensive actions.
8. **Validate:** Re-run the workflow on a second synthetic dataset and confirm that the same rules produce explainable results.

## 6. Commands and tools
Example safe workspace commands:

```bash
mkdir -p data/{raw,processed} evidence reports src
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
sha256sum data/raw/* 2>/dev/null
```

For structured data inspection:

```bash
python - <<'PY'
import json
from pathlib import Path
for path in Path("data/raw").glob("*.json"):
    records = json.loads(path.read_text())
    print(path.name, "records:", len(records) if isinstance(records, list) else 1)
PY
```

Adapt the analysis tooling to the project question. Use read-only queries and synthetic inputs; do not run scans or tests against systems outside the authorized scope.

## 7. Expected output
- A documented lab layout and reproducible analysis notes.
- A normalized dataset or clearly described analytical result.
- An evidence register with source, timestamp, confidence, and limitations.
- A short report containing the question, method, observations, assessment, and next steps.
- Three simulated training illustrations: workflow, analysis view, and validation view.

## 8. Findings and risk assessment
For each observation, record: evidence ID, observed fact, source, first-seen/last-seen time, confidence rationale, relevance, potential impact, and alternative explanation. Separate confirmed facts from analyst hypotheses. Explain false-positive risks and stale-data risks. Do not claim a compromise based only on an IOC match or public reputation score.

## 9. Framework mapping
Where applicable, map supported behavior to **MITRE ATT&CK** tactics/techniques and relevant **CWE/OWASP** categories only when they genuinely fit. For intelligence lifecycle work, document direction, collection, processing, analysis, dissemination, and feedback. Include framework version and mapping rationale.

## 10. Remediation and defensive recommendations
Recommend proportionate controls based on evidence: validate telemetry, tune detections, block or monitor indicators only after review, improve logging, update playbooks, and communicate uncertainty. Include an owner, priority, and target date for each recommendation.

## 11. Validation and success criteria
- Inputs are traceable, checksummed, and clearly labeled as real public source or simulated.
- The workflow is reproducible and produces consistent output on the supplied test data.
- Every conclusion links to evidence and explains confidence and limitations.
- False positives and benign explanations are considered.
- Recommendations are actionable and can be validated by a second analyst.

## 12. Evidence and reporting checklist
- [ ] Scope, authorization, and question recorded
- [ ] Data sources, dates, terms, and checksums documented
- [ ] Raw data preserved; transformations repeatable
- [ ] Findings linked to evidence and confidence rationale
- [ ] ATT&CK/framework mappings justified or marked not applicable
- [ ] Recommendations, validation results, and limitations included

## 13. Deliverables
Commit the sanitized report, scripts, schema, and synthetic sample data to this project folder. Never commit secrets, personal data, customer telemetry, or restricted source content.

---
*Training note: all diagrams in this folder are simulated illustrations, not actual tool screenshots or evidence from a live investigation.*
