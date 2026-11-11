# QC_REPORT.md — Master Quality Control Scorecard (`game-modding`)

- **qc_status**: `PENDING_FIRST_ROUND` *(Values: `PENDING_FIRST_ROUND` | `PASS` | `REFINEMENT_REQUIRED`)*
- **overall_score**: `TBD` *(Must be `>= 8.5 / 10.0` AND all 5 categories `>= 8.5 / 10.0` to `PASS`)*
- **round_number**: `0` *(Max 3 auto-refinement rounds per milestone)*
- **last_audited**: `YYYY-MM-DD`
- **auditor**: `master-qc-director` *(Single Master QC Sub-Agent)*

---

## 1. 5-Pillar Quality Scorecard (Strict `>= 8.5 / 10` Floor Per Category)

| # | Category *(Defined in `.ai/QUALITY_CONTROL.md`)* | Score (`/ 10.0`) | Gate (`>= 8.5`) | Key Deductions & Evidence Summary |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Visual / 3D Model / Art / UI Polish** | `TBD` | `PENDING` | *Not audited yet* |
| **2** | **Mechanics / Interaction Feel / Ergonomics** | `TBD` | `PENDING` | *Not audited yet* |
| **3** | **Code Architecture & Anti-Bloat Compliance** | `TBD` | `PENDING` | *Not audited yet* |
| **4** | **Features & Scope Completeness** | `TBD` | `PENDING` | *Not audited yet* |
| **5** | **Performance, Build & Runtime Stability** | `TBD` | `PENDING` | *Not audited yet* |
| — | **OVERALL AVERAGE** | **`TBD`** | **`PENDING`** | **Requires Overall >= 8.5 AND Every Category >= 8.5** |

---

## 2. Concrete Evidence Inspected
- **Build / Compiler / Test Output**: *(Pending)*
- **Visual / 3D Viewport / UI Inspection** *(e.g. Blender MCP `look`, Chrome DevTools MCP, Compose Preview, Screenshots)*: *(Pending)*
- **Files & Assets Audited**: *(Pending)*

---

## 3. Mandatory Refinements Required (When Any Category `< 8.5 / 10`)
> **Instruction for Main Agent**: If `qc_status` is `REFINEMENT_REQUIRED`, you MUST resolve every item below and re-run the single `master-qc-director` check (up to 3 rounds max) before declaring the task complete.

- [ ] *(Populated by `master-qc-director` during audit)*

---

## 4. Round History Log
| Round | Date | Overall Score | Lowest Category | Verdict | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `0` | `YYYY-MM-DD` | `TBD` | `TBD` | `PENDING_FIRST_ROUND` | Initial template state |
