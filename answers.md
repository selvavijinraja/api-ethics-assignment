# Task 1 — Classify and Handle PII Fields

The dataset contains the following fields:  
`full_name, email, date_of_birth, zip_code, job_title, diagnosis_notes`

### Classification
- **Direct PII** → full_name (pseudonymize), email (drop)  
- **Indirect PII** → date_of_birth, zip_code, job_title, diagnosis_notes (mask/generalize)  

### Handling Table

| Field           | Type of PII | Action        | Justification |
|-----------------|-------------|---------------|---------------|
| full_name       | Direct PII  | Pseudonymize  | Replace with random codes to preserve linkage but protect identity. |
| email           | Direct PII  | Drop          | Direct identifier, not needed for analysis. |
| date_of_birth   | Indirect PII| Mask          | Keep only year or age range to reduce re‑identification risk. |
| zip_code        | Indirect PII| Mask          | Generalize to region or first 3 digits. |
| job_title       | Indirect PII| Mask          | Broaden to categories (e.g., “Healthcare worker”). |
| diagnosis_notes | Indirect PII| Mask/Redact   | Free text may contain identifiers; redact sensitive info. |

---

# Task 2 — Audit the API Script for Ethical Compliance

Your team's data collection script:

```python
import requests

API_URL = "https://healthstats-api.example.com/records"
API_KEY = "free_tier_key_abc123"

records = []
for page in range(1, 101):
    response = requests.get(API_URL, params={"page": page, "key": API_KEY})
    data = response.json()
    records.extend(data["results"])

# Store all records permanently in company database
save_to_database(records)
Violations and Fixes
Using a free‑tier API key for bulk commercial collection

Problem: The script loops through 100 pages with a free‑tier key. Free tiers are meant for limited, non‑commercial use. Collecting large datasets for company use violates the API’s terms of service.

Correction: Upgrade to a paid/commercial license and use the proper key.

python
API_KEY = "commercial_tier_key_xyz789"  # upgraded license
response = requests.get(API_URL, params={"page": page, "key": API_KEY})
Permanently storing API response data

Problem: The script saves all records permanently in the company database. Most APIs restrict how long you can retain or cache their data. Permanent storage breaches the TOS and raises privacy concerns.

Correction: Store only what is permitted (e.g., aggregate statistics or temporary cache), and respect retention limits.

python
# Example: store only aggregated counts, not raw records
for page in range(1, 101):
    response = requests.get(API_URL, params={"page": page, "key": API_KEY})
    data = response.json()
    process_and_store_summary(data["results"])  # summaries, not raw permanent storage
Or, if caching is allowed for a limited time:

python
cache_records_temporarily(records, expiry_days=30)