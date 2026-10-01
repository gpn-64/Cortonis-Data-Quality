# 🧪 Regulatory Data Quality Dashboard

A Power BI dashboard for monitoring the **data quality of regulatory information** (RIM) in a pharmaceutical company: QC checks run across Registrations, Submissions, Products and Documents, the deviations they raise, and how fast those deviations get corrected.

---

## ⚠️ Everything here is synthetic

This is a **portfolio project**. None of it is real.

- **The data is 100% synthetic.** The 12,000-row export in `data/raw/` was generated for this project. It is not an extract from any real system and contains no real regulatory records.
- **"Cortonis Pharma" is a fictional company.** It does not exist. The persona shown in the report (`William User / william.user@cortonis.com`), the team names and the org structure are all invented.
- **The QC checks are invented.** The 26 checks in this project (see [below](#the-qc-checks)) were written from scratch to look plausible. They do **not** necessarily reflect the checks, thresholds, priorities or risk ranking that a real pharma regulatory / data-governance function would use. Treat them as an illustrative catalogue, not a recommendation.

---

## About

Regulatory Information Management (RIM) systems hold the master data that authorises a company to sell a product in a country: registrations, submissions, applications, health-authority correspondence, controlled documents. When that data drifts — an orphaned registration, a duplicate submission ID, an approval dated before its submission — the business risk is real (missed renewals, non-compliant filings, audit findings).

This project models a recurring **QC-check process** over that data and builds the dashboard a data-governance lead would use to run it:

- **Overview** — *How compliant is our regulatory data overall?*
- **Findings** — the check-level list of current findings, each linked to its record.
- **Process & Checks** — *Which processes and fields generate the most findings?*
- **Quality Deviations** — *Which findings are still open, and how fast do we close them?*
- **EDA** (hidden) — free pivot tables for ad-hoc exploration.

---

## Screenshots

### Overview
Headline KPIs (compliance rate, current findings, open and aging deviations, MTTR, right-first-time), monthly check volume by compliance status, and a compliance breakdown that pivots across dimensions.

![Overview](<reports/screenshots/1_Overview.PNG>)

### Findings
Every current finding with its deviation, DQ dimension, country, criticality, RIM process area, check and product, plus a link to the source record.

![Findings](<reports/screenshots/2_Findings.PNG>)

### Process & Checks
Compliance rate and non-compliant checks per RIM process area and check, average findings detected per month, and detected vs corrected findings over time.

![Process & Checks](<reports/screenshots/3_Process and Checks.PNG>)

### Quality Deviations
Deviation register with correction progress, resolution-time histogram (mean vs median time to resolve), and the open-deviation backlog by RIM process area.

![Quality Deviations](<reports/screenshots/4_Quality Deviations.PNG>)

---

## The data model, and what is deliberately *not* in this project

The single flat table this dashboard consumes (`data/raw/data export quality dashboard (fictional v2).csv`) is the **target shape** — the clean, check-level fact table you would want in order to monitor data quality and build a dashboard on top of it. One row = one QC check executed against one record, with its outcome, its deviation (if any), the detection and correction dates, and the process / product / country / team it belongs to.

**Producing that table is the actual hard part, and it is out of scope here.** In a real setup you would have to:

- pull records out of one or more RIM systems and their satellites (submissions archive, document management, product master data);
- reconcile entities across those systems (a registration in one, its documents in another, its submissions in a third);
- encode each QC rule as executable logic and run it on a schedule;
- open, route, track and close deviations, and capture the correction date.

This repository starts *after* all of that: it assumes the check-level table already exists and focuses on the semantic model and the report. The data-engineering pipeline that would build the table for real is intentionally not included.

---

## RIM data aligned to the DIA RIM Reference Model

The model is named against the **DIA RIM Reference Model V2.0** (DIA RIM Working Group, 2026 — copy in [`docs/dia standards/`](<docs/dia%20standards/>)), the industry's vendor-neutral reference framework for regulatory information, **not** against any single RIM product's object model. The QC checks are phrased the same way (e.g. *"Broken link Submission → Application → Registration"*, *"Registration without linked Health Authority"*).

| In this project                                                                                                                                | DIA RIM Reference Model V2.0                                                                                                                                                 | Note                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `Object = Submission`                                                                                                                        | **Submission**                                                                                                                                                         | exact object name                                                                                                            |
| `Object = Registration`                                                                                                                      | **License-Registration**                                                                                                                                               | DIA's full object name; "Registration" is the common industry short form                                                     |
| `Object = Product`                                                                                                                           | **Medicinal Product** (in the Product Family → Global Product → Medicinal Product hierarchy)                                                                         | kept as the umbrella term                                                                                                    |
| `Object = Document`                                                                                                                          | **Content** / **Submission Content**                                                                                                                             | documents are formally scoped to the sister*DIA EDM Reference Model*; "Document" is the term every RIM/DMS platform shares |
| `Application`, `Health Authority`, `Content Plan`, `Product Family`, `Active Substance`, `Procedure Type`, `Country`, `Region` | Application · Health Authority · Submission Content Plan · Product Family · Substance / "INN (generic name)" · Application Procedure Type · Country · Country.Regions | all DIA object / attribute names                                                                                             |
| `Process` ∈ {Submission / Registration / Product Management, Document Control}                                                              | regulatory business-process capability names                                                                                                                                 | standard RIM capability taxonomy, not vendor-specific                                                                        |
| `Dimension` ∈ {Completeness, Uniqueness, Validity, Accuracy, Consistency, Timeliness, Referential Integrity}                                | *not a DIA concept*                                                                                                                                                        | the six**DAMA-DMBOK** data-quality dimensions, plus Referential Integrity                                              |

The Registration / Submission / Application trio is **shared vocabulary** between the DIA model and every major RIM vendor, so the same fields map — with only a rename — onto:

- **Veeva Vault RIM** (Registrations / Submissions / Submissions Archive)
- **Ennov RIM**
- **ArisGlobal LifeSphere RIM**
- **Calyx RIM**
- **Generis CARA RIM**
- **EXTEDO RIMS**
- **Lorenz** (drugTrack / docuBridge)
- **Samarind RMS**
- **Amplexor / Acolad Life Sciences RIM**

No feature of the report depends on a vendor-specific schema, and no term used here is unique to Veeva Vault RIM.

Known wording drift from the strict DIA vocabulary (kept for readability, no impact on portability): `Submission ID` → DIA *Submission Number*; `Registration Number` → DIA *License Number*; `Type of Product` carries therapeutic classes and would be *Therapeutic Area* in DIA (and *Antipiretics* should read *Antipyretics*).

---

## Data source

**Synthetic** — `data/raw/data export quality dashboard (fictional v2).csv`

|                 |                                                                                           |
| --------------- | ----------------------------------------------------------------------------------------- |
| Rows            | 12,000 (one per QC check)                                                                 |
| Detection dates | 2023-09-01 → 2026-08-20                                                                  |
| Countries       | 134, grouped into 5 regions                                                               |
| Teams           | 20 (4 functions × 5 regions)                                                             |
| Distinct checks | 26, across 7 data-quality dimensions                                                      |
| Processes       | 4 — Submission Management, Registration Management, Product Management, Document Control |
| Products        | 240, across 6 therapeutic classes                                                         |
| Findings        | ~826 detected / ~833 corrected / ~10,341 with no finding                                  |

### Columns (raw export)

| Field                                                       | Description                                                                                  |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `Check Name`                                              | The QC rule that was run                                                                     |
| `Dimension`                                               | Completeness, Referential Integrity, Uniqueness, Consistency, Timeliness, Validity, Accuracy |
| `Object` / `Field`                                      | Regulatory object and field the rule targets                                                 |
| `Process`                                                 | Business process the check belongs to                                                        |
| `Criticality`                                             | Critical / Major / Minor                                                                     |
| `Check Status`                                            | `No finding` · `Finding detected` · `Finding corrected`                              |
| `Compliance Status`                                       | `Compliant` / `Non compliant` (derived from `Check Status`)                            |
| `Deviation #`                                             | Deviation identifier, when a finding is raised                                               |
| `Detection Date` / `Compliance Date` / `Created Date` | Finding QC checks lifecycle dates                                                           |
| `Product` / `Type of Product`                           | Affected product and its therapeutic class                                                   |
| `Country` / `Region`                                    | Where the affected record is registered                                                      |
| `Team`                                                    | Team responsible for the process in that region                                              |
| `Record ID` / `Finding ID`                              | Record and finding keys                                                                      |

### The QC checks

The 26 invented checks, by process:

- **Registration Management** — Orphaned Registration after Product merge/deletion · Duplicate Registration Number within same country/product · Registration without linked Product · Registration without linked Health Authority · Registration linked to archived/inactive Health Authority · Registration status vs linked document status mismatch · Renewal completed but entered beyond SOP-defined entry window
- **Submission Management** — Submission without linked Application · Broken link Submission → Application → Registration · Duplicate Submission ID from bulk import · Submission missing Content Plan · Submission tracking status inconsistent with Application status · Submission event recorded beyond SOP-defined entry window · Approval date earlier than submission date · Approval date in metadata mismatched vs Health Authority approval letter · Health Authority confirmation date mismatch vs recorded date
- **Product Management** — Product record missing INN/generic name · Product name/spelling inconsistent across linked records · Duplicate Product/Country/Procedure combination · Deprecated reference value still in use · Country/Health Authority outside reference model
- **Document Control** — Multiple documents simultaneously marked "Approved" · Approved document missing effective date · Approved document not uploaded/indexed within SOP-defined timeframe · Document language inconsistent with "Language" metadata field · Document orphaned after Registration archival

---

## Semantic model

Star schema, Import mode, one flat source table split into a fact and three dimensions in Power Query.

```
fact_qcchecks ──┬── dim_process    (Check Name → Process, Criticality, Dimension, Field, Object, Team)  via "Check Name - Country"
                ├── dim_countries  (Country → Region)
                ├── dim_products   (Product → Type of Product)
                └── Detection / Compliance / Created Date  (auto date tables)

X-Axis Switch   field parameter — lets most charts pivot their axis across 13 dimensions
```

### Key DAX measures (`_Measures`)

| Measure                                         | Definition                                                                       |
| ----------------------------------------------- | -------------------------------------------------------------------------------- |
| `Total Checks`                                | `DISTINCTCOUNT(fact_qcchecks[Record ID])`                                      |
| `Compliant Checks` / `Non-Compliant Checks` | `Total Checks` filtered on `Compliance Status`                               |
| `Compliance Rate %`                           | `DIVIDE([Compliant Checks], [Total Checks])`                                   |
| `Open Deviations`                             | distinct`Deviation #` where `Check Status = "Finding detected"`              |
| `Deviations Corrected`                        | checks where`Check Status = "Finding corrected"`                               |
| `Total Deviations`                            | distinct`Deviation #` where `Check Status <> "No finding"`                   |
| `Deviation Rate %`                            | `DIVIDE([Total Deviations], [Total Checks])`                                   |
| `Correction Rate %`                           | `DIVIDE([Deviations Corrected], [Total Deviations])`                           |
| `Avg Days to Correct`                         | `AVERAGEX` of `DATEDIFF(Detection, Compliance, DAY)` over corrected findings |
| `Critical Open Deviations`                    | `Open Deviations` where `Criticality = "Critical"`                           |
| `Right First Time %`                          | share of checks where`Compliance Date = Created Date`                          |

> **Note:** `Non-Compliant Checks` equals `Open Deviations` by construction — `Compliance Status` is fully derived from `Check Status` in the synthetic data. `Deviation Rate %` and `1 − Compliance Rate %` are *not* the same thing: the first counts every historical deviation (including corrected ones), the second is a current-state snapshot.

---

## Repository structure

```
Data-Quality/
├── data/
│   ├── raw/         # the synthetic check-level export (source of the model)
│   ├── processed/   # (unused — no transformation layer in this project)
│   └── sample/      # tiny placeholder sample
├── dashboard/
│   ├── powerbi/     # Power BI project in PBIP format (JSON + TMDL, diffable)
│   │   ├── Data Quality Dashboard.pbip
│   │   ├── Data Quality Dashboard.Report/         # pages & visuals (PBIR)
│   │   └── Data Quality Dashboard.SemanticModel/  # model & Power Query M (TMDL)
│   ├── assets/      # page-background source images
│   └── tableau/     # (unused)
├── docs/            # references & bibliography (+ data-dictionary / methodology templates)
├── sql/ src/ scripts/ notebooks/   # scaffolding only — see "out of scope" above
├── reports/screenshots/   # report page captures (shown above)
└── LICENSE
```

The `sql/`, `src/`, `scripts/` and `notebooks/` folders are repo scaffolding kept from a template. They hold no logic here — the data-operations work they would contain is deliberately **out of scope** (see [above](#the-data-model-and-what-is-deliberately-not-in-this-project)).

---

## Opening the project

1. Clone the repo.
2. Open `dashboard/powerbi/Data Quality Dashboard.pbip` in **Power BI Desktop** (with *Power BI Project (.pbip)* save format enabled).
3. The model imports from the CSV in `data/raw/` via an absolute path in `expressions.tmdl` — update that path to your local clone, then **Refresh**.

---

## References

Full bibliography — DIA RIM Reference Model V2.0, data-quality frameworks (DAMA-DMBOK,
ISO 8000), the regulatory standards the checks assume (eCTD, IDMP, SPOR, INN), RIM
vendor references and build tooling — in [`docs/references.md`](docs/references.md).

---

## License

MIT — see [LICENSE](LICENSE).
