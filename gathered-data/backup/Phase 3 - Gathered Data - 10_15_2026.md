# Phase 3: Leave Management — Gathered Data & Business Requirements
**Date of Gathering:** October 15, 2026  
**Document Status:** Polished & Enhanced  
**Primary Architecture Reference:** [`../system-flow/Phase 3_ High-Level System Flow v5.png`](file:///C:/Users/mananap/Development/vaults/hrms-leave-management-vault/system-flow/Phase%203_%20High-Level%20System%20Flow%20v5.png)  
**Detailed Domain Specification:** [`Phase 3 - Enhanced Gathered Data & System Specification.md`](file:///C:/Users/mananap/Development/vaults/hrms-leave-management-vault/gathered-data/Phase%203%20-%20Enhanced%20Gathered%20Data%20&%20System%20Specification.md)  
**Legal References:** [`../legal-basis/`](file:///C:/Users/mananap/Development/vaults/hrms-leave-management-vault/legal-basis) (Omnibus Rules on Leave, CSC Res. 2100020, CSC-DBM JC 1 s. 2006, etc.)  
**Document Templates:** [`../doc-templates/`](file:///C:/Users/mananap/Development/vaults/hrms-leave-management-vault/doc-templates) (CS Form 6/6a, MRATU, SRATU, CETO, Ledgers)

---

## 1. High-Level System Architecture & Flow

Aligned with **System Flow v5**, the Leave Management module encompasses four functional pillars:
1. **1.1 Employee Leave Credits**: View leave types/requirements, single-pane credit dashboard, and manual (calamity) vs. automated (monthly & validated lifecycle) crediting.
2. **1.2 Leave Applications**: Leave creation (CS Form 6, Monetization, TLB), late filing watermarking, 5-stage approval routing, and post-approval modifications.
3. **1.3 Leave Data Management**: Role-based access (Employee View, Admin Officer View, HR Admin CRUD) for Leave Ledgers and COC/ETO Ledgers.
4. **1.4 Reports**: Compliance generation (MRATU, SRATU, CETO, Certificate of Earned Credits, Work Schedule Master).

---

## 2. Leave Application Process Flow & Signatory Hierarchy

### 2.1 5-Stage Application Lifecycle
1. **Employee**: Submits Leave Application via the portal or manual encoding (Item 1 to 6.D).
2. **Admin Officer (AO)**: Reviews and executes **Certification of Leave Credits** (Item 7.A: balances of VL and SL as of filing date).
3. **Department Head**: Reviews application and provides **Recommendation** (Item 7.B: For Approval or For Disapproval).
   > **UI Formatting Rule**: If the Department Head recommends **disapproval**, the recommendation text and status must be rendered in **RED FONT**.
4. **HR (CHRMO)**: Quality audit and verification of application details, documentary attachments, and statutory compliance.
5. **Agency Head (Approving Authority)**: Final action (Item 7.C Approved / Item 7.D Disapproved).

### 2.2 Signatory Routing Matrix

| Personnel Hierarchy | First Signatory / Certification | Second Signatory / Recommendation | Final Approving Authority |
| :--- | :--- | :--- | :--- |
| **Executive Branch (Rank & File, Dept Heads)** | Department AO | Department Head | **City Mayor** |
| **Legislative Branch (SP Rank & File, SP Heads)** | SP Admin Officer | Secretary to the Sangguniang Panlungsod | **City Vice Mayor** |
| **City Vice Mayor** | CHRMO Head / AO | City Administrator (Noted) | **City Mayor** |
| **City Mayor** | CHRMO Head | City Administrator (Noted) | **DILG Regional Director / Secretary** |

### 2.3 Alternate / Delegated Signatures
- **OIC Signatory Support**: In the event of travel, official business, or absence of the City Mayor or Vice Mayor, the system supports designation of an **Alternate / Officer-In-Charge (OIC) Signatory** based on an official Office Order.
- **Revocation Rule**: The delegation requires **manual revocation** by the HR Admin (it does not automatically expire; it stays active until manually revoked upon the principal official's return).
- The generated leave form printout dynamically displays: *"For: [Official Name], [Title] by [Designated OIC], [Designation Order No.]"*.

### 2.4 Application Status States
- **Approved**: Granted with pay, without pay, or other conditions.
- **Disapproved**: Formally rejected with reason indicated under Item 7.D.
- **Refile**: Returned to applicant for necessary correction or missing documentary attachments.
- **Cancelled**: Officially recalled or employee-cancelled prior to or during the leave period.

---

## 3. Leave Form Specifications (CS Form No. 6 Mapping)

### 3.1 Commutation Selection (Item 6.D)
- **"Not Requested"**: Selected by default for all typical leave applications (vacation, sick, mandatory, special privileges, etc.).
- **"Requested"**: Selected strictly for:
  - **Monetization of Leave Credits**
  - **Terminal Leave Benefit (TLB)**

### 3.2 Sick Leave Late Filing Flag & Watermark (Item 7.D / UI Input)
- Sick leave must be filed immediately upon the employee's return to duty, with a maximum filing allowance of **five (5) days after the affected days of leave**.
- If an employee files a sick leave application exceeding **5 days after the inclusive leave dates**:
  - The application is **automatically flagged as Late Filing**.
  - A prominent **"LATE FILING" watermark** is reflected beneath its input field on screen and on the generated CS Form No. 6.
  - The entry is logged as late filing and displayed in **red font** in the employee's Leave Ledger card.

---

## 4. Leave Ledger & Accrual Rules

### 4.1 Leave Without Pay (LWOP) Impact on Accrual
- Standard accrual rate: $1.25\text{ days VL} + 1.25\text{ days SL}$ per month.
- If an employee incurs Leave Without Pay (LWOP):
  - Monthly accrual is reduced proportionately according to CSC Omnibus Rules Table III:
    $$\text{Accrual} = \frac{\text{Days Present}}{30} \times 1.25$$
  - **CGB Core Rule**: The proportional reduction resulting from LWOP **only affects the Vacation Leave (VL) credit accrual**. The Sick Leave (SL) credit accrual remains unaffected.

### 4.2 Non-Earning Leaves with Pay
The following statutory leaves are with full pay, but **do not earn leave credits (VL/SL)** during the duration of the leave:
1. **Special Leave Benefits for Women (Magna Carta for Women - R.A. 9710)** (Up to 2 months post-surgery)
2. **Rehabilitation Privilege (Sec. 55, Rule XVI)** (Up to 6 months for work-connected injuries)

*Behavioral Note*: These are the only leaves that behave like LWOP in terms of credit accrual suspension, while remaining fully paid leaves.

### 4.3 Deductions for Tardiness and Undertime
- Working hours converted per CSC Table IV: $1\text{ hour} = 0.125\text{ day}$, $1\text{ minute} = 0.002083\text{ day}$.
- Tardiness and undertime are **strictly deducted from Vacation Leave (VL)** credits.
- Under no circumstances is tardiness/undertime charged to Sick Leave (SL) unless backed by a medical certificate.
- In the Leave Ledger card, all tardiness, undertime, and late filing entries are rendered in **RED FONT**.

---

## 5. Monetization of Leave Credits

- **Vacation Leave Exhaustion Condition**: An employee **may only monetize Sick Leave (SL) credits if their Vacation Leave (VL) credits are already fully exhausted**, and subject to formal written authorization by the **City Mayor**.
- Standard minimum monetization: 10 days, provided 5 days VL is maintained.

---

## 6. Post-Approval Modification Lifecycles

### 6.1 Recall & Restoration Process Flow (VL and FL Only)
1. **Trigger**: Operational exigency where the department urgently requires the presence of an employee on approved Vacation Leave or Forced Leave.
2. **Department Recommendation**: Department Head submits a recall request with formal justification.
3. **Mayor Approval**: For review and approval by the **City Mayor**.
4. **Administrative Memo Generation**: System generates the official **Recall Memorandum**.
5. **Ledger Restoration**: Recalled/unused leave credits are restored to the employee's Leave Ledger with notation citing the memo.

### 6.2 Cancellation Process Flow (Advance Filing & Sick Leave)
1. **Trigger**: Employee cancels an advance-filed leave or unused approved leave.
2. **Request**: Employee submits cancellation request via portal.
3. **Department Head Approval**: Approved directly by the **Department Head**.
4. **Ledger Restoration**: Deducted leave credits are returned to the active leave ledger.

### 6.3 Reschedule Process Flow (Advance Filing & Sick Leave)
1. **Trigger**: Employee requests shifting approved dates.
2. **Request**: Employee submits reschedule request with new proposed dates.
3. **Department Head Approval**: Approved directly by the **Department Head**. Inclusive dates updated in system.

### 6.4 Automatic Restoration for Declared Holidays
- **Full-Day Holiday**: If a non-working holiday is declared during an approved leave window, the system automatically restores the $1.0\text{ day}$ leave credit to the ledger.
- **Half-Day Holiday**:
  - The system **restores the entire whole-day equivalent ($1.0\text{ day}$)** of leave credit to the employee.
  - The system automatically flags the employee's attendance record with **undertime or tardiness** corresponding to the half-day session not covered by the declared holiday.

---

## 7. Downstream Administrative Impact & Integrations

### 7.1 Service Record
- The system automatically logs every period of **Leave Without Pay (LWOP)** into the employee's official **Service Record**.

### 7.2 Notice of Step Increment (NOSI) Postponement
- **Policy Rule**: If an employee incurs cumulative Leave Without Pay (LWOP) of **15 days or more** during the step period, the effectivity of the Step Increment is postponed.
- **Calculation Basis**:
  $$\text{Adjusted NOSI Date} = \text{Original NOSI Date} + \text{Total Days of LWOP}$$
- **Example**:
  - Original NOSI Effectivity: **January 15, 2026**
  - Accumulated LWOP: **30 days**
  - Adjusted NOSI Effectivity: **February 14, 2026**

### 7.3 Automated Notification of AWOL
- **Policy Rule**: Unapproved, unauthorized continuous absences.
- **Automated Threshold**: If cumulative AWOL reaches **20 days in a single calendar month**, the system triggers an immediate **automated high-priority alert to the HR Admin** for issuance of a Return-to-Work notice and initiation of dropping from the rolls.

---

## 8. Personnel Scope: Non-Government Service Personnel (COS / JO)

Non-Government Service Personnel do not earn statutory civil service leave credits. Their attendance and compensatory privileges are managed through:
1. **Overtime Request Form** (`forms__overtime-request-form.docx`): Pre-approval of overtime work.
2. **Certificate of Earned Time-Off (CETO)** (`certificates__certificate-of-earned-time-off-(CETO).docx`): Formal monthly certification of accumulated offset hours.
3. **Time Offset Application** (`forms__time-offset-application.docx`): Application to utilize earned offset hours against absences.
4. **Earned Time-Off Ledger** (`reports__earned-time-off-ledger.docx`): Offset ledger maintaining balance of earned vs. availed offset hours.
