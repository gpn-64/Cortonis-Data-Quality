# References & bibliography

Sources behind the data model, the naming conventions, the QC-check catalogue and the
dashboard build. Everything the project *produces* is synthetic (see the main
[README](../README.md)); the items below are the real-world frameworks it borrows its
vocabulary and structure from.

---

## 1. Regulatory Information Management — data model & terminology

### DIA RIM Reference Model V2.0 *(primary reference)*

The `Object` / `Field` names, the entity relationships and the wording of the QC checks are
aligned to this framework.

- **DIA RIM Reference Model V2.0** — DIA RIM Reference Model Working Group, Final,
  created 2025-10-28, modified 2026-04-13. Distributed under the Creative Commons
  Attribution License.
  - *User Guide* — [`dia standards/RIM-Reference-Model-User-Guide.pdf`](<dia%20standards/RIM-Reference-Model-User-Guide.pdf>)
  - *Conceptual Entity-Relationship model* — [`dia standards/RIM-Reference-Model-V20-Conceptual-ER-Model.pdf`](<dia%20standards/RIM-Reference-Model-V20-Conceptual-ER-Model.pdf>)
  - *Data dictionary workbook* (56 objects, attributes, controlled-vocabulary examples) —
    [`dia standards/RIM-Reference-Model-V20.xlsx`](<dia%20standards/RIM-Reference-Model-V20.xlsx>)
  - Change requests / governance: LinkedIn group *DIA Regulatory Information Management*.
- **DIA — Drug Information Association** — [https://www.diaglobal.org/](https://www.diaglobal.org/) · Regulatory Affairs
  Community (RAC), which hosts the RIM Working Group.
- **DIA RIM White Paper / book** — *Achieving Excellence with Regulatory Information
  Management* (RIM White Paper v3.0), DIA RIM Working Group.

Sister DIA reference models (document/metadata-centric — cited for scope boundary, the
`Document` object in this project formally belongs here rather than in RIM):

- **DIA EDM (Electronic Document Management) Reference Model.**
- **DIA TMF (Trial Master File) Reference Model** — now under CDISC.

---

## 2. Data quality — dimensions & governance

The `Dimension` column (Completeness, Uniqueness, Validity, Accuracy, Consistency,
Timeliness, Referential Integrity) comes from general data-quality practice, **not** from DIA.

- **DAMA-DMBOK2** — *Data Management Body of Knowledge*, 2nd ed., DAMA International,
  Technics Publications, 2017 — ch. 13, Data Quality (dimensions of data quality).
- **DAMA UK Working Group** — *The Six Primary Dimensions for Data Quality Assessment*
  (2013).
- **ISO 8000** — Data quality (esp. 8000-8, information and data quality: concepts and
  measuring).
- **ISO/IEC 25012** — Data quality model (inherent vs. system-dependent characteristics).
- **EDM Council — DCAM** (Data Management Capability Assessment Model) — data-quality
  management practices.
- **Data Quality - Empowering businesses with analytics and AI** - Prashanth Southekal

---

## 3. Regulatory standards referenced inside the QC checks

Controlled vocabularies and formats the checks assume (e.g. *"Country/Health Authority
outside reference model"*, *"Submission Format = eCTD"*, *"missing INN/generic name"*).

- **ICH M8 — eCTD** (electronic Common Technical Document) and regional eCTD
  specifications.
- **ISO IDMP** — Identification of Medicinal Products: ISO 11615 (regulated medicinal
  product information), 11616 (pharmaceutical product), 11238 (substances), 11239, 11240.
- **EMA SPOR** — Substance, Product, Organisation, Referential master data services
  (incl. OMS — Organisation Management Service — for Health Authority / organisation data).
- **WHO INN** — International Nonproprietary Names for pharmaceutical substances.
- **ISO 3166** — country codes.
- **ISO 8601** — date format (`YYYY-MM-DD`), used throughout the model.

---

## 4. RIM platforms — market context

The dashboard is designed to be vendor-neutral (see *RIM-agnostic by design* in the
README). Vendor product lines referenced there, for context only:

- **Veeva Vault RIM** — [https://www.veeva.com/products/vault-rim/](https://www.veeva.com/products/vault-rim/)
- **Ennov RIM** — [https://www.ennov.com/](https://www.ennov.com/)
- **ArisGlobal LifeSphere RIM** — [https://www.arisglobal.com/](https://www.arisglobal.com/)
- **Calyx RIM** — [https://calyx.ai/](https://calyx.ai/)
- **Generis CARA RIM** — [https://www.generis.com/](https://www.generis.com/)
- **EXTEDO RIMS / eCTDmanager** — [https://www.extedo.com/](https://www.extedo.com/)
- **LORENZ drugTrack / docuBridge** — [https://www.lorenz.cc/](https://www.lorenz.cc/)
- **Samarind RMS** — [https://www.samarind.co.uk/](https://www.samarind.co.uk/)
- **Amplexor / Acolad Life Sciences RIM** — [https://www.acolad.com/](https://www.acolad.com/)

Market framing for RIM as a capability: Gartner *Market Guide for Regulatory Information
Management*; DIA RIM maturity discussions.
