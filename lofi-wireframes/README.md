# Low-Fidelity Wireframes – Phase 3 Leave Management

Traditional box-type, grayscale wireframes for the CGB-HRMS Leave Management module. They were drawn independently from:

- `gathered-data/Phase 3 - Enhanced Gathered Data & System Specification.md`
- `system-flow/Phase 3 - Comprehensive System Breakdown & Process Flows.md` (+ System Flow v5 diagram)

The earlier work in `/design` and `/wireframes` was not used.

**Open:** `index.html` in any browser. It's a single file with no dependencies.

## Screen index

| # | Screen | Flow box | Process | Roles |
|---|---|---|---|---|
| 00 | Home Dashboard | — | — | All |
| 01 | Leave Types Catalog | 1.1.1 | P1 | EMP, AO |
| 02 | Leave Type Details (modal) | 1.1.1.1 | P1 | EMP, AO |
| 03 | Actual Leave Credits – Single Pane | 1.1.2.1–1.1.2.4 | P2 | EMP, AO, CHRMO |
| 04 | Crediting – Automated Runs | 1.1.2.5.1 (auto) | P3, P4 | CHRMO |
| 05 | Crediting – Calamity Batch (SEL) | 1.1.2.5.1 (manual) | P5 | CHRMO |
| 06 | My Leave Applications | 1.2.1 | — | EMP, AO, CHRMO |
| 07 | File Leave (CS Form 6) | 1.2.2 / 1.2.2.1 | P6 | EMP |
| 07A | Form – Common Data Inventory (spec) | 1.2.2.1 | P6 | — |
| 07B | Leave Application Form – Common Base | 1.2.2.1 | P6 | EMP |
| 08 | Monetization / TLB variant | 1.2.2 | P8, P9 | EMP, CHRMO |
| 09 | Application Details | 1.2.1.1 | — | All |
| 10 | Approval Queue | 1.2.2.2 | P7 | AO, DH, CHRMO, APR |
| 11 | Review & Act (7.A–7.D) | 1.2.2.2 | P7 | AO, DH, CHRMO, APR |
| 12 | Modify Approved Leave (Cancel/Reschedule) | 1.2.3 / 1.2.3.1 | P11 | EMP → DH |
| 13 | Recall Request (VL/FL) | 1.2.3.1 | P10 | DH → Mayor |
| 14 | Leave Credits Management | 1.3.1 | P13 | CHRMO |
| 15 | Leave Ledger Card | 1.3.2 | P13 | EMP/AO view, CHRMO CRUD |
| 16 | COC / CTO Ledger (Track A) | 1.3.3 | P14 | EMP/AO view, CHRMO CRUD |
| 17 | Overtime & Time Offset (Track B) | 1.1.2.4 / 1.3.3 | P15 | COS/JO, DH, CHRMO |
| 18 | MRATU / SRATU | 1.4.1 | P16 | AO, DH, CHRMO |
| 19 | Certifications | 1.4.2 | P17 | EMP, CHRMO |
| 20 | Work Schedule & DTR Rectification | 1.4.3 | P18 | AO, EMP, DH, CHRMO |
| 21 | Holiday Calendar & Collision Restoration | Settings | P12 | CHRMO |
| 22 | Alternate Signatory (OIC) | 1.2.2.2 | — | CHRMO |
| 23 | Alerts – AWOL & NOSI | Integr. 6.1/6.2 | P19, P20 | CHRMO |
| 24 | Leave Type Setup – List | Settings (feeds 1.1.1) | — | CHRMO |
| 25 | Leave Type Builder (create/edit, e.g. Wellness Leave) | Settings (feeds 1.1.1, 1.1.2, 1.2.2) | — | CHRMO |

## Interpretation decisions

- **One shared app shell.** A left nav grouped by the four v5 branches, plus an Admin group for Settings and Alerts. Role-gated items are marked `*`.
- **One app, role-aware.** There are no separate apps per role. Panels change with the user's role (e.g. the employee picker on 03, and the tier panels on 11).
- **Track B (COS/JO)** users see a reduced experience: ETO, Time Offset and CETO only, with no VL/SL screens.
- **Red-font rule** applies throughout: late filing, tardiness/undertime, LWOP and DH disapproval.
- **Calamity crediting** is a 4-step wizard (event → scope → preview → confirm), because it changes many records at once.
- **Leave types are configurable data, not a fixed list.** The common attributes in 07A are the schema behind the Leave Type Builder (25). When a new issuance arrives (e.g. a Wellness Leave), CHRMO configures it, and it appears in the catalog, the single pane, the application form, the ledger and the reports. The 15 statutory types ship as built-in records whose core calculations are locked.
- **Holiday restoration** and **automated accrual** are system jobs. Their screens are for monitoring and preview, with no manual "run" button.
