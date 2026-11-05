# CGB-HRMS Phase 3: System Flow Decomposition & Process Specifications

## Granular Breakdown of System Flow v5 & End-to-End Process Workflows

> **System:** City Government of Butuan Human Resource Management System (CGB-HRMS)  
> **Module Scope:** Phase 3 – Leave Management & Compensatory Time-Off  
> **Reference Model:** `Phase 3_ High-Level System Flow v5.png`  
> **Legal Baseline:** CSC Omnibus Rules on Leave (Rule XVI, E.O. 292 / CSC MC No. 41, s. 1998 as amended), CSC Res. 2100020 (Expanded Maternity Leave), CSC-DBM JC No. 1, s. 2006 (COC/CTO), COA-DBM JC No. 2, s. 2020 (COS/JO).

---

## 1. Complete Structural Decomposition of System Flow Boxes

The diagram below mirrors and expands every single box and leaf node identified in **Phase 3 High-Level System Flow v5**:

```mermaid
flowchart TD
    Root["1. LEAVE MANAGEMENT"]

    %% Tier 1
    Root --> M1["1.1 Employee Leave Credits"]
    Root --> M2["1.2 Leave Applications"]
    Root --> M3["1.3 Leave Data Management"]
    Root --> M4["1.4 Reports"]

    %% 1.1 Branch
    M1 --> B1_1["1.1.1 Different Types of Leave"]
    B1_1 --> B1_1_1["1.1.1.1 View Instructions & Requirements per Leave Type"]

    M1 --> B1_2["1.1.2 Actual Leave Credits (Single Pane View)"]
    B1_2 --> B1_2_1["1.1.2.1 Basic & Mandatory (VL, SL, FL)"]
    B1_2 --> B1_2_2["1.1.2.2 Special Privileges & Family (SLP, ML, PL, SPL)"]
    B1_2 --> B1_2_3["1.1.2.3 Special Emergency & Statutory (SEL, Rehab, Magna Carta, VAWC, Study)"]
    B1_2 --> B1_2_4["1.1.2.4 Compensatory Time-Off (CTO) & Time Offset (TO)"]
    B1_2 --> B1_2_5["1.1.2.5 Creation/Modification of Leave Crediting"]
    B1_2_5 --> B1_2_5_1["1.1.2.5.1 Manual vs. Automated Granting"]

    %% 1.2 Branch
    M2 --> B2_1["1.2.1 Employee Leave Applications"]
    B2_1 --> B2_1_1["1.2.1.1 View Leave Application Details"]
    M2 --> B2_2["1.2.2 Creation of Leave Application (Inc. Monetization & TLB)"]
    B2_2 --> B2_2_1["1.2.2.1 Input Details (CS Form 6 Mapping)"]
    B2_2 --> B2_2_2["1.2.2.2 Compliance & Approval (5-Tier Chain)"]
    M2 --> B2_3["1.2.3 Modification of Approved Leave"]
    B2_3 --> B2_3_1["1.2.3.1 Request & Admin Approval (Dept Head + HR Admin)"]

    %% 1.3 Branch
    M3 --> B3_1["1.3.1 Employee Leave Credits Management (HR Admin)"]
    M3 --> B3_2["1.3.2 Employee Leave Ledger Management (Employee: View | AO: View | HR: CRUD)"]
    M3 --> B3_3["1.3.3 COC & Earned Time-Off (ETO) Ledger Management (Employee: View | AO: View | HR: CRUD)"]

    %% 1.4 Branch
    M4 --> B4_1["1.4.1 Regulatory Compliance Reports (MRATU Regular/Casual, SRATU)"]
    M4 --> B4_2["1.4.2 Official Certifications (Earned Credits, CETO)"]
    M4 --> B4_3["1.4.3 Operational Schedules (Work Schedule Master, DTR Rectification)"]
```

---

## 2. Granular Box Breakdown & Specifications

### Box 1.1: Employee Leave Credits
Central repository and engine for tracking, presenting, and granting employee leave entitlements.

*   **Box 1.1.1: Different Types of Leave**
    *   **Scope:** Global catalog of statutory and administrative leaves recognized under Philippine Civil Service laws and local CGB policies.
    *   **Components:** 15 distinct leave categories (Vacation, Sick, Forced/Mandatory, Maternity, Paternity, Solo Parent, Special Privilege, Study, VAWC, Rehabilitation, Magna Carta for Women, Calamity/SEL, Adoption, Monetization, Terminal Leave).
    *   **Box 1.1.1.1: View Instructions & Requirements per Leave Type**
        *   **Role:** Employee Self-Service (ESS) and Administrative Officer (AO) reference modal.
        *   **Data Fields:** Legal citation, filing window requirements (e.g., 5 days advance for VL, within 30 days for Calamity), mandatory documentary attachments (e.g., Medical Certificate, Barangay Calamity Declaration, Solo Parent ID), pay status (with pay vs. without pay), and credit-earning rules.

*   **Box 1.1.2: Actual Leave Credits (Single Pane View)**
    *   **Scope:** Unified real-time dashboard displaying all leave credit balances for an individual employee.
    *   **Box 1.1.2.1: Basic & Mandatory Leave**
        *   Vacation Leave (VL) balance (cumulative).
        *   Sick Leave (SL) balance (cumulative).
        *   Mandatory / Forced Leave (FL) balance (5-day annual quota; tracks used, remaining, and auto-forfeiture status).
    *   **Box 1.1.2.2: Special Privileges & Family Leave**
        *   Special Privilege Leave (SPL) balance (3 days non-cumulative).
        *   Maternity Leave (ML) balance / active entitlement window (105 / 120 / 60 days).
        *   Paternity Leave (PL) balance (7 days non-cumulative; capped at first 4 deliveries).
        *   Solo Parent Leave (SPL) balance (7 days non-cumulative; tied to annual ID validity).
    *   **Box 1.1.2.3: Special Emergency & Statutory Leave**
        *   Special Emergency Leave (SEL / Calamity) balance (up to 5 days per disaster).
        *   Rehabilitation Privilege (up to 6 months; non-earning status flag).
        *   Magna Carta for Women (up to 2 months post-surgery; non-earning status flag).
        *   10-Day VAWC Leave (10 days; confidentiality-protected).
        *   Study Leave (up to 6 months; contract-linked).
    *   **Box 1.1.2.4: Compensatory Time-Off (CTO) & Time Offset (TO)**
        *   Track A (Plantilla/Casual): Compensatory Overtime Credits (COC) converted to CTO in hours/days (1-year validity).
        *   Track B (COS/JO): Earned Time-Off (ETO) balance in hours based on approved Overtime Request Forms.
    *   **Box 1.1.2.5: Creation/Modification of Leave Crediting**
        *   **Box 1.1.2.5.1: Manual vs. Automated Granting**
            *   *Manual Trigger (Admin)*: Used for Special Emergency (Calamity) Leave. HR Admin initiates batch crediting upon formal LGU/NDRRMC calamity declaration.
            *   *Automated Trigger (System)*:
                1. Monthly Accrual: End-of-month crediting of 1.25 VL and 1.25 SL, automatically adjusted for Leave Without Pay (LWOP).
                2. Lifecycle Validation: Conditional statutory leaves (ML, PL, Magna Carta) are automatically credited into the active balance once the leave application is approved by the City Mayor / Vice Mayor.

---

### Box 1.2: Leave Applications
Core operational subsystem handling employee requests, compliance checks, routing chains, and post-approval adjustments.

*   **Box 1.2.1: Employee Leave Applications**
    *   Application tracker repository with real-time status indicators (`Draft`, `Submitted`, `Certified`, `Recommended`, `CHRMO Verified`, `Approved`, `Disapproved`, `Refile`, `Recalled`, `Cancelled`).
    *   **Box 1.2.1.1: View Leave Application Details**
        *   Detailed CS Form No. 6 view rendering historical approvals, digital signatures, attached proof documents, and tracking audit log.

*   **Box 1.2.2: Creation of Leave Application (Inc. Monetization & Terminal Leave Benefit)**
    *   Entry point for all leave requests, including standard leaves, monetization, and retirement commutation.
    *   **Box 1.2.2.1: Provide/Input Leave Application Details (CS Form No. 6 Mapping)**
        *   Item 6.A (Leave Type), Item 6.B (Details/Destination/Medical condition), Item 6.C (Number of working days & inclusive dates).
        *   Item 6.D (Commutation): Default `"Not Requested"`; automatically forced to `"Requested"` when filing for Monetization or Terminal Leave Benefit (TLB).
        *   *Late Filing & Filing Window Detection*: Dynamic calculation comparing the date of filing against statutory leave filing rules:
            *   *Sick Leave (SL)*: Can be filed in advance (for scheduled medical procedures/examinations or doctor-advised rest) or post-absence upon return to duty. For post-absence filings, sick leave filed **more than 5 days after the affected inclusive leave dates** automatically triggers an indelible **"LATE FILING" watermark** beneath the input field/Item 6.C and on the generated CS Form No. 6 printout, and flags the entry for **red font** rendering in the leave ledger card.
            *   *Statutory Advance Leaves*: Vacation Leave and Solo Parent Leave require filing at least 5 days in advance; Maternity Leave requires at least 30 days advance notice (except emergency); Calamity Leave within 30 days from occurrence.
            *   *Documentary Thresholds*: Sick leave exceeding 5 successive days or involving hospitalization/out-patient care strictly requires a Physician's Medical Certificate attachment.
    *   **Box 1.2.2.2: Compliance & Approval (5-Tier Chain)**
        *   Tier 1: Employee Submission.
        *   Tier 2: Admin Officer (Item 7.A - Certification of Available Credits).
        *   Tier 3: Department Head (Item 7.B - Recommendation; **Disapproval rendered in RED FONT**).
        *   Tier 4: CHRMO Audit (Policy validation, documentary completeness).
        *   Tier 5: City Mayor / City Vice Mayor / DILG (Item 7.C Approved / Item 7.D Disapproved).
        *   *Delegated / Alternate (OIC) Signatory Management*: Activated by HR Admin pursuant to an official Office Order. **Operates under Manual Revocation** (the delegation remains strictly active across all relevant approval queues until HR Admin manually revokes the designation in the system upon the principal's resumption of duty). Dynamically renders: *"For: [Official Name], [Title] by [Designated OIC], [Designation Order No.]"*.

*   **Box 1.2.3: Modification of Approved Leave**
    *   **Box 1.2.3.1: Employee Request and Admin Approval**
        *   *Recall Flow (VL & FL only)*: Operational exigency recall initiated by Dept Head, approved by City Mayor, generating formal Administrative Recall Memo, and restoring unused credits.
        *   *Cancellation Flow*: Advance-filed or unused approved leaves cancelled by employee, approved by Dept Head, restoring leave credits.
        *   *Rescheduling Flow*: Change of inclusive dates approved by Dept Head without balance alteration.
        *   *Automatic Holiday Restoration*: Automatic system cancellation of leave deduction when a non-working holiday collides with an approved leave. Full-day restores 1.0 day; Half-day restores 1.0 day and flags attendance with half-day undertime/tardiness.

---

### Box 1.3: Leave Data Management
Master administration hub controlling ledgers, audit cards, credit adjustments, and role-based permissions.

*   **Box 1.3.1: Employee Leave Credits Management**
    *   Administrative interface for initial balance onboarding, annual Forced Leave forfeiture, and ad-hoc credit corrections.
*   **Box 1.3.2: Employee Leave Ledger Management**
    *   Lifelong digital Leave Ledger Card (`reports__leave-ledger.xlsx`).
    *   RBAC: Employee (View), AO (View Dept), HR Admin (CRUD / Full Override).
    *   Automated mathematical conversion engine (CSC Tables I–IV):
        *   Tardiness/undertime conversion ($0.125/\text{hr}$, $0.002083/\text{min}$) strictly deducted from Vacation Leave.
        *   LWOP proportional credit reduction affecting **only Vacation Leave**.
        *   All tardiness, undertime, and late filing entries formatted in **RED FONT**.
*   **Box 1.3.3: Compensatory Overtime Credits (COC) & Earned Time-Off (ETO) Ledger Management**
    *   Track A: COC/CTO Ledger under CSC-DBM JC No. 1, s. 2006 (tracks earned overtime multiplier $1.0\times$ or $1.5\times$, max 120 hours ceiling, 1-year expiration).
    *   Track B: Earned Time-Off Ledger (`reports__earned-time-off-ledger.docx`) for COS/JO personnel tracking overtime against Time Offset applications.
    *   RBAC: Employee (View), AO (View Dept), HR Admin (CRUD).

---

### Box 1.4: Reports
Reporting and certification engine delivering all regulatory documents and operational tools.

*   **Box 1.4.1: Regulatory Compliance Reports**
    *   Monthly Report on Absence, Tardiness & Undertime (MRATU): Dual-sheet output (**Regular MRATU** and **Casual MRATU**) directly exported to payroll.
    *   Summary Report on Absences, Tardiness & Undertime (SRATU): Department-level monthly transmittal signed by Dept Head.
*   **Box 1.4.2: Official Certifications**
    *   Certificate of Earned Leave Credits: Formal certification of accumulated credits for transfer, resignation, or retirement.
    *   Certificate of Earned Time-Off (CETO): Monthly certification of approved compensatory hours for COS/JO personnel.
*   **Box 1.4.3: Operational Schedules & Exception Management**
    *   Work Schedule Master (`reports__work-schedule.xlsx`): Department shift schedules and flexitime definitions.
    *   DTR Rectification Form (`forms__dtr-rectification-form.xlsx`): Biometric punch failure validation and attendance reconciliation.

---

## 3. End-to-End Process Flows (Per Identified Process)

---

### Process 1: Employee Leave Catalog & Requirements Inquiry
*   **System Box:** `1.1.1` & `1.1.1.1`
*   **Trigger:** Employee or Department AO needs to determine applicable leave type, statutory filing rules, or documentary requirements.
*   **Actors:** Employee (ESS), Admin Officer (AO).

```mermaid
flowchart TD
    Start(["Employee / AO Opens Portal"]) --> Navigate["Navigate to 1.1.1 Different Types of Leave"]
    Navigate --> SelectType["Select Target Leave Type (e.g., ML, VAWC, Magna Carta, Study)"]
    SelectType --> DisplayDetails["System Renders Interactive Specification Modal:<br/>- Legal Basis Citation<br/>- Maximum Allotment & Pay Rules<br/>- Statutory Advance Notice Window<br/>- Mandatory Documentary Attachments<br/>- Credit Accrual Eligibility (Earning vs Non-Earning)"]
    DisplayDetails --> ActionChoice{"Employee Next Action?"}
    ActionChoice -->|"Download Checklist / Forms"| DownloadDoc["Download Sample / CS Form 6a"]
    ActionChoice -->|"Proceed to File"| RouteToFile["Pre-populate Item 6.A in CS Form 6 Filing Portal"]
    ActionChoice -->|"Close"| Done(["Exit Modal"])
```

---

### Process 2: Actual Leave Credits Dashboard (Single-Pane View)
*   **System Box:** `1.1.2`, `1.1.2.1` to `1.1.2.4`
*   **Trigger:** User accesses dashboard to check current balances prior to filing leave or conducting monthly audit.
*   **Actors:** Employee (Self), Admin Officer (Dept View), HR Admin (Global View).

```mermaid
flowchart TD
    Start(["Access Single-Pane Leave Dashboard"]) --> AuthCheck{"User Role"}
    AuthCheck -->|"Employee"| LoadSelf["Fetch Own Employee ID"]
    AuthCheck -->|"AO"| LoadDept["Select Employee within Department"]
    AuthCheck -->|"HR Admin"| LoadGlobal["Search Any CGB Employee Record"]

    LoadSelf & LoadDept & LoadGlobal --> QueryLedger[("Query Active Leave Ledger & ETO Ledger")]

    QueryLedger --> RenderPane["Render Consolidated Dashboard:"]
    
    subgraph DashboardView ["Single Pane Display"]
        direction TB
        P1["1.1.2.1 Basic & Mandatory:<br/>VL Balance | SL Balance | FL Balance (Used/Forfeited)"]
        P2["1.1.2.2 Special Privileges & Family:<br/>SPL (3d) | ML Window | PL (7d) | Solo Parent (7d)"]
        P3["1.1.2.3 Special Emergency & Statutory:<br/>Calamity (SEL) | Rehab Privilege | Magna Carta | VAWC | Study"]
        P4["1.1.2.4 Compensatory Credits:<br/>Track A: CTO Balance (Hours/Days)<br/>Track B (COS/JO): Earned Time-Off Balance"]
    end

    RenderPane --> DashboardView
    DashboardView --> End(["Display Ready / Export Summary"])
```

---

### Process 3: Standard Monthly Accrual & LWOP Proration Engine
*   **System Box:** `1.1.2.5.1 (Automated)` & `1.3.2**`**
*   **Trigger:** Automated cron trigger at 23:59 on the last calendar day of each month.
*   **Actors:** Automated System Engine, HR Admin (Auditor).

```mermaid
flowchart TD
    Start(["Scheduled Monthly Accrual Trigger (End of Month)"]) --> FetchEmps["Query Active Plantilla, Casual, and Contractual Personnel"]
    FetchEmps --> LoopEmp["Evaluate Next Employee Record"]

    LoopEmp --> CheckNonEarning{"Is Employee on Non-Earning Leave?<br/>(Magna Carta for Women or Rehab Privilege)"}
    CheckNonEarning -->|"Yes"| SkipAccrual["Log in Ledger: Accrual Suspended (Under RA 9710 / Sec. 55)<br/>Credits Earned = 0.000 VL, 0.000 SL"] --> CheckNext
    CheckNonEarning -->|"No"| CheckService["Calculate Days of Actual Service in Month"]

    CheckService --> CheckMidMonth{"Mid-Month Entry / Separation?"}
    CheckMidMonth -->|"Yes"| TableII["Apply CSC Table II Proration:<br/>Credits = round(Days of Service / 24, 3)"]
    CheckMidMonth -->|"No"| CheckLWOP{"Did Employee Incur LWOP in Current Month?"}

    CheckLWOP -->|"No LWOP"| StandardCredit["Grant Standard Accrual:<br/>+1.250 VL<br/>+1.250 SL"]
    CheckLWOP -->|"Yes, Has LWOP"| TableIII["Apply CSC Table III & CGB Business Rule:<br/>Days Present = 30 - Total LWOP Days<br/>Adjusted VL = (Days Present / 30) * 1.25<br/>Adjusted SL = 1.250 (Unaffected)"]

    TableII & StandardCredit & TableIII --> PostLedger["Append New Line to Employee Leave Ledger Card:<br/>- Credit Added<br/>- Updated Total Balances<br/>- Timestamp & Auto-Certification"]

    PostLedger --> CheckNext{"More Employees?"}
    CheckNext -->|"Yes"| LoopEmp
    CheckNext -->|"No"| NotifyHR["Generate Monthly Accrual Audit Summary to HR Admin"] --> End(["End of Accrual Cycle"])
```

---

### Process 4: Conditional Statutory Lifecycle Crediting
*   **System Box:** `1.1.2.5.1 (Automated)` & `1.2.2.2`
*   **Trigger:** City Mayor / Vice Mayor approves statutory application (Maternity, Paternity, Magna Carta, Solo Parent).
*   **Actors:** Approving Authority, System Engine, Employee.

```mermaid
flowchart TD
    Start(["Final Approval of Statutory Leave Application"]) --> InspectType{"Identify Statutory Leave Type"}

    InspectType -->|"Maternity Leave (RA 11210)"| CheckMLType{"Delivery Classification"}
    CheckMLType -->|"Live Birth"| Credit105["Credit 105 Calendar Days"]
    CheckMLType -->|"Solo Mother"| Credit120["Credit 120 Calendar Days (105 + 15)"]
    CheckMLType -->|"Miscarriage / Termination"| Credit60["Credit 60 Calendar Days"]

    InspectType -->|"Paternity Leave (RA 8187)"| CheckPLQuota{"Check Delivery Counter"}
    CheckPLQuota -->|"Count <= 4"| CreditPL["Credit 7 Working Days PL"]
    CheckPLQuota -->|"Count > 4"| RejectPL["Disapprove: Exceeded statutory 4-delivery cap"]

    InspectType -->|"Magna Carta for Women (RA 9710)"| CreditMCW["Credit Approved Surgical Recovery Window (Up to 2 Months)<br/>Activate Accrual Suspension Flag"]

    InspectType -->|"Solo Parent Leave (RA 8972)"| CheckSPID{"Verify Annual ID Expiry"}
    CheckSPID -->|"Valid"| CreditSPL["Credit 7 Working Days SPL"]
    CheckSPID -->|"Expired"| BlockSPL["Require Annual Solo Parent ID Renewal"]

    Credit105 & Credit120 & Credit60 & CreditPL & CreditMCW & CreditSPL --> ActivateLeave["Bind Credits to Leave Window & Update Single-Pane View"]
    ActivateLeave --> NotifyApplicant["Notify Employee & AO of Available Statutory Credits"] --> End(["Lifecycle Crediting Complete"])
    RejectPL & BlockSPL --> End
```

---

### Process 5: Batch Calamity Leave Crediting (Special Emergency Leave - SEL)
*   **System Box:** `1.1.2.5.1 (Manual Form)`
*   **Trigger:** Official declaration of State of Calamity by City Mayor, Sangguniang Panlungsod, or NDRRMC.
*   **Actors:** HR Admin, City Mayor / Sangguniang Panlungsod, Department AO.

```mermaid
flowchart TD
    Start(["Calamity Declaration Issued (Typhoon, Flood, Earthquake)"]) --> AdminOpen["HR Admin Opens Manual Crediting Module (1.1.2.5.1)"]
    AdminOpen --> InputEvent["Input Calamity Parameters:<br/>- Calamity Event Name & SP Resolution / Order No.<br/>- Date of Calamity<br/>- Affected Geographic Barangays / Zones<br/>- Allotted Days (Standard: 5 Working Days)"]
    InputEvent --> SelectTarget{"Target Employee Scope"}
    SelectTarget -->|"All City Employees"| SelectAll["Batch Select All Active Personnel"]
    SelectTarget -->|"Specific Affected Barangays"| FilterGeo["Filter Personnel by Registered Home Address"]

    SelectAll & FilterGeo --> PreviewBatch["Generate Crediting Preview List"]
    PreviewBatch --> ConfirmBatch["HR Admin Confirms Batch Execution"]
    ConfirmBatch --> ExecuteCrediting["System Credits 5 Days SEL to Selected Accounts:<br/>- Validity: 30 days from calamity occurrence<br/>- Ledger Notation: Credited per Res. No. [XXXX]"]
    ExecuteCrediting --> BroadcastNotice["Broadcast System Notification to Employees & AOs to file SEL"] --> End(["Batch SEL Crediting Complete"])
```

---

### Process 6: Leave Application Submission & Validation (CS Form No. 6)
*   **System Box:** `1.2.1`, `1.2.2`, `1.2.2.1`
*   **Trigger:** Employee initiates a leave request.
*   **Actors:** Employee (Applicant), System Validation Engine.

```mermaid
flowchart TD
    Start(["Employee Initiates CS Form No. 6 Filing"]) --> Step6A["Select Leave Type (Item 6.A)"]
    Step6A --> CheckCommutation{"Is Filing for Monetization or TLB?"}

    %% Commutation Flow (Monetization & TLB)
    CheckCommutation -->|"Yes"| SetCommutationReq["Item 6.D Commutation = 'Requested'<br/>(Inclusive Dates Omitted; Input Desired Days)"]
    SetCommutationReq --> ValidateMonetization{"Check Monetization Rules:<br/>1. Minimum 10 Days<br/>2. Retain >= 5 Days VL Balance<br/>3. SL Monetized ONLY if VL Exhausted"}
    ValidateMonetization -->|"Invalid"| WarnMonetization["Block / Warn: Violates Monetization Rules"] --> Step6A
    ValidateMonetization -->|"Valid"| ValidateBalance{"Check Preliminary Leave Balance"}

    %% Standard Absence Leave Flow
    CheckCommutation -->|"No"| SetCommutationNotReq["Item 6.D Commutation = 'Not Requested'"]
    SetCommutationNotReq --> Step6B["Provide Specific Details (Item 6.B):<br/>- Destination (Local / Abroad)<br/>- Illness / Treatment details<br/>- Study / Exam details"]
    Step6B --> Step6C["Input Number of Working Days & Inclusive Dates (Item 6.C)"]

    Step6C --> CheckLeaveType{"Is Leave Type = Sick Leave (SL)?"}

    %% Sick Leave Path
    CheckLeaveType -->|"Yes"| CheckSLTiming{"Sick Leave Timing"}
    CheckSLTiming -->|"In Advance (Scheduled Exam / Surgery / Bed Rest)"| CheckSLMedCert{"Leave Duration > 5 Successive Days<br/>OR Hospital / Out-Patient?"}
    CheckSLTiming -->|"Post-Absence (Upon Return to Duty)"| CheckSLLate{"Is Filing Date > 5 Days<br/>After Affected Leave Dates?"}

    CheckSLLate -->|"Yes (Late Filing)"| ApplyWatermark["System Triggers Late Filing Rules:<br/>1. Apply indelible 'LATE FILING' watermark on screen & CS Form 6<br/>2. Flag entry for RED FONT display in leave ledger card"] --> CheckSLMedCert
    CheckSLLate -->|"No (On-Time Filing)"| CheckSLMedCert

    CheckSLMedCert -->|"Yes"| RequireMedCert["Mandatory Attachment:<br/>Physician Medical Certificate"] --> VerifyAttachments
    CheckSLMedCert -->|"No"| VerifyAttachments

    %% Other Leave Types Path
    CheckLeaveType -->|"No"| CheckFilingWindow{"Validate Statutory Filing Window:<br/>- VL / Solo Parent: >= 5 Days Advance<br/>- Maternity: >= 30 Days Advance (except emergency)<br/>- Calamity (SEL): <= 30 Days from Event"}
    CheckFilingWindow --> VerifyAttachments{"Verify Required Attachments per Leave Type"}

    %% Attachment Verification & Submission
    VerifyAttachments --> CheckDocType{"Attachment Status"}
    CheckDocType -->|"Missing"| PromptUpload["Prompt Mandatory Upload<br/>(e.g., Med Cert, Travel Authority, Solo Parent ID)"] --> Step6B
    CheckDocType -->|"Complete"| ValidateBalance

    ValidateBalance -->|"Insufficient Balance"| WarnEmployee["Warn: Request exceeds credits.<br/>Excess will be converted to LWOP."] --> ConfirmSubmission
    ValidateBalance -->|"Sufficient Balance"| ConfirmSubmission["Employee Signs & Submits Application"]

    ConfirmSubmission --> LockDraft["Lock Application State -> Submitted<br/>Route to Department Admin Officer (Tier 2)"] --> End(["Application Lodged in Routing Queue"])
```

---

### Process 7: 5-Tier Review, Certification & Approval Workflow
*   **System Box:** `1.2.2.2`
*   **Trigger:** Successful submission of CS Form No. 6.
*   **Actors:** Employee, Admin Officer (AO), Department Head, CHRMO Head, City Mayor / Vice Mayor / Alternate Signatory.

```mermaid
sequenceDiagram
    autonumber
    actor EMP as 1. Employee
    actor AO as 2. Admin Officer (Item 7.A)
    actor DH as 3. Department Head (Item 7.B)
    actor CHRM as 4. CHRMO Compliance
    actor MAYOR as 5. Approving Authority (Mayor/Vice Mayor/OIC)

    EMP->>AO: Submit CS Form 6 Application
    Note over AO: Step 1: Open Application in Queue<br/>Verify Leave Ledger Balances as of Filing Date
    AO->>AO: Fill Item 7.A Certification:<br/>- VL Balance & SL Balance<br/>- Sign Certification
    AO->>DH: Forward Certified Form to Department Head

    Note over DH: Step 2: Review Operational Impact & Urgency<br/>Determine Recommendation (Item 7.B)
    alt Department Head Recommends Disapproval
        DH->>DH: Render Recommendation in RED FONT<br/>State Justification for Disapproval
    else Department Head Recommends Approval
        DH->>DH: Render Recommendation in Normal Font
    end
    DH->>CHRM: Transmit Recommended Application to CHRMO

    Note over CHRM: Step 3: CHRMO Quality Audit<br/>- Statutory Compliance Verification<br/>- Check Documentary Authenticity<br/>- Verify Signatory Routing Chain
    CHRM->>MAYOR: Transmit Verified Application to Approving Authority

    Note over MAYOR: Step 4: Final Action (Item 7.C / 7.D)<br/>Check Delegated / OIC Signatory (Active until Manually Revoked by HR Admin)
    alt Final Action: Approved
        MAYOR->>MAYOR: Specify Days with Pay / Days without Pay<br/>Execute Digital Signature
        MAYOR-->>EMP: Application Status: APPROVED
        Note over EMP: System notifies Employee & deducts/allocates credits
    else Final Action: Disapproved
        MAYOR->>MAYOR: Formulate Item 7.D Reason for Disapproval
        MAYOR-->>EMP: Application Status: DISAPPROVED
    else Needs Amendment
        MAYOR-->>EMP: Application Status: REFILE (Returned for Corrections)
    end
```

---

### Process 8: Leave Monetization Lifecycle
*   **System Box:** `1.2.2` & Section 6.4
*   **Trigger:** Employee requests monetization during official monetization window.
*   **Actors:** Employee, Department AO, CHRMO, City Mayor.

```mermaid
flowchart TD
    Start(["Employee Files Leave Monetization Application"]) --> CheckComm["Item 6.D Commutation set to 'Requested'"]
    CheckComm --> InputDays["Input Requested Monetization Days (Minimum: 10 Days)"]
    InputDays --> CheckVLReserve{"Check Vacation Leave (VL) Balance"}

    CheckVLReserve -->|"VL Balance - Requested < 5.0 Days"| BlockVL["Block Request:<br/>CSC Rule: Must retain at least 5.0 days VL balance"] --> End(["Application Disallowed"])
    CheckVLReserve -->|"VL Balance - Requested >= 5.0 Days"| CheckSLMonetize{"Does Application Include Sick Leave (SL) Monetization?"}

    CheckSLMonetize -->|"No (Pure VL)"| CheckFiftyPercent
    CheckSLMonetize -->|"Yes (Monetizing SL)"| CheckVLExhaustion{"Is Vacation Leave Fully Exhausted?"}

    CheckVLExhaustion -->|"VL Not Exhausted"| BlockSL["Block SL Monetization:<br/>CGB Rule: SL can ONLY be monetized if VL is fully exhausted"] --> End
    CheckVLExhaustion -->|"VL Fully Exhausted"| VerifyMayorConsent["Require Formal Written Justification & Direct Mayor Approval"] --> CheckFiftyPercent

    CheckFiftyPercent{"Is Monetization > 50% of Accumulated Credits?"}
    CheckFiftyPercent -->|"Yes (>50%)"| RequireJustification["Require Medical / Calamity / Educational Proof"] --> RouteApproval
    CheckFiftyPercent -->|"No (<=50%)"| RouteApproval["Route to AO Certification -> CHRMO Verification -> City Mayor Approval"]

    RouteApproval --> MayorDecision{"Mayor Final Action"}
    MayorDecision -->|"Approved"| DeductCredits["Deduct Monetized Days from Ledger:<br/>1. Deduct from VL balance<br/>2. Deduct from SL balance (if exhausted VL & approved)"]
    DeductCredits --> TransmitPayroll["Transmit Approved Commutation Voucher to City Accounting & Payroll"] --> End(["Monetization Disbursed"])
    MayorDecision -->|"Disapproved"| End
```

---

### Process 9: Terminal Leave Benefit (TLB) Processing
*   **System Box:** `1.2.2` & Section 7
*   **Trigger:** Employee separation from government service (Retirement, Resignation, Death).
*   **Actors:** Retiring/Separating Employee, CHRMO Records Officer, City Mayor, City Accounting.

```mermaid
flowchart TD
    Start(["Employee Separation Trigger (Retirement / Resignation)"]) --> InitiateTLB["Initiate Terminal Leave Application (CS Form No. 6)"]
    InitiateTLB --> AutoCommutation["Force Item 6.D Commutation to 'Requested'"]
    AutoCommutation --> AttachDocs["Attach Mandatory Clearance Requirements:<br/>- CGB Property & Money Clearance<br/>- Official Service Record<br/>- Ombudsman Clearance<br/>- CSC Retirement Order / Acceptance of Resignation"]

    AttachDocs --> AuditLedger["CHRMO Conducts Complete Audit of Lifelong Leave Ledger Card"]
    AuditLedger --> CalculateCredits["Compute Total Commutable Leave Credits:<br/>Total Days = Final Cumulative VL Balance + Final Cumulative SL Balance"]
    CalculateCredits --> FormulaCheck["Apply DBM Constant Monetization Formula:<br/>TLB Amount = Total Commutable Days * Daily Salary Rate"]

    FormulaCheck --> MayorApproval["City Mayor Executes Formal TLB Approval"]
    MayorApproval --> CloseLedger["Close Employee Leave Ledger Card:<br/>- Post Full Commutation Deduction<br/>- Final Balances Zeroed Out<br/>- Status Marked: 'Separated / Ledger Closed'"]
    CloseLedger --> TransmitDisbursement["Forward Approved TLB Voucher & Ledger to Payroll for Disbursement"] --> End(["TLB Complete"])
```

---

### Process 10: Approved Leave Recall & Restoration Process (VL & FL Only)
*   **System Box:** `1.2.3` & `1.2.3.1`
*   **Trigger:** Unforeseen operational exigency requiring an employee on Vacation or Forced Leave to return to duty.
*   **Actors:** Department Head, City Mayor, HR Admin, Employee.

```mermaid
flowchart TD
    Start(["Urgent Operational Exigency Occurs in Department"]) --> DHInit["Department Head Initiates Recall Request"]
    DHInit --> CheckLeaveType{"Is Approved Leave Vacation (VL) or Forced Leave (FL)?"}
    CheckLeaveType -->|"No (SL, ML, etc.)"| RejectRecall["Recall Disallowed:<br/>Sick, Maternity, and Special Privileges cannot be recalled"] --> End(["Exit Flow"])
    CheckLeaveType -->|"Yes (VL or FL)"| SpecifyDates["Specify Recalled Inclusive Dates & Operational Justification"]

    SpecifyDates --> SubmitMayor["Submit Recall Recommendation to City Mayor"]
    SubmitMayor --> MayorDecision{"City Mayor Action"}
    MayorDecision -->|"Disapproved"| NotifyDH["Notify Department Head: Recall Denied"] --> End
    MayorDecision -->|"Approved"| GenerateMemo["System Generates Official Administrative Recall Memo<br/>(Numbered & Formatted)"]

    GenerateMemo --> ServeMemo["Serve Recall Memo to Employee & Department Head"]
    ServeMemo --> RestoreCredits["System Restores Unused Recalled Leave Credits to Leave Ledger:<br/>- Balance Restored<br/>- Ledger Notation: 'Recalled per Memo No. [XXXX]'"]
    RestoreCredits --> ResetFL{"Was Recalled Leave Forced Leave (FL)?"}
    ResetFL -->|"Yes"| ProtectFL["Protect FL from Forfeiture:<br/>Recalled FL credits remain active and will not be forfeited at year-end"]
    ResetFL -->|"No"| EndRecall(["Recall Completed & DTR Resumed"])
    ProtectFL --> EndRecall
```

---

### Process 11: Approved Leave Cancellation & Rescheduling
*   **System Box:** `1.2.3` & `1.2.3.1`
*   **Trigger:** Employee requests cancellation or date modification of an approved leave.
*   **Actors:** Employee, Department Head, HR Admin.

```mermaid
flowchart TD
    Start(["Employee Opens Approved Leave Record"]) --> SelectAction{"Select Modification Type"}

    %% Cancellation Branch
    SelectAction -->|"Cancellation"| InputCancelReason["Input Cancellation Justification & Dates"]
    InputCancelReason --> SubmitCancelDH["Route Cancellation Request to Department Head"]
    SubmitCancelDH --> DHApproveCancel{"Department Head Decision"}
    DHApproveCancel -->|"Disapproved"| KeepApproved["Application Remains Approved as Scheduled"] --> End(["Exit Flow"])
    DHApproveCancel -->|"Approved"| SystemRestore["System Restores Leave Credits to Ledger:<br/>- Status Updated: CANCELLED<br/>- Deducted credits returned to active VL/SL balance"] --> NotifyCancel["Send Notification to Employee, AO, and CHRMO"] --> End

    %% Reschedule Branch
    SelectAction -->|"Rescheduling"| InputNewDates["Input Proposed New Inclusive Dates"]
    InputNewDates --> ValidateOverlap{"Check Attendance Overlap & Working Calendar"}
    ValidateOverlap -->|"Collision Detected"| ErrorConflict["Prompt Conflict Warning"] --> InputNewDates
    ValidateOverlap -->|"Clear"| SubmitRescheduleDH["Route Reschedule Request to Department Head"]
    SubmitRescheduleDH --> DHApproveResched{"Department Head Decision"}
    DHApproveResched -->|"Disapproved"| KeepApproved
    DHApproveResched -->|"Approved"| UpdateDates["Update Inclusive Dates in Master Leave Record:<br/>- Ledger balance remains bracketed<br/>- Shift Schedule adjusted in DTR system"] --> NotifyResched["Send Confirmation Notification"] --> End
```

---

### Process 12: Automatic Holiday Collision & Restoration Rule
*   **System Box:** `1.2.3` & Section 6.4
*   **Trigger:** Declaration of a local or national non-working holiday that falls on dates of already-approved leave.
*   **Actors:** HR Admin (Declares Holiday in Calendar), Automated Leave Engine, DTR System.

```mermaid
flowchart TD
    Start(["Holiday Declared & Published in System Calendar"]) --> ScanCollisions["Engine Scans Active Approved Leave Applications for Matching Dates"]
    ScanCollisions --> CollisionFound{"Approved Leave Collides with Holiday?"}
    CollisionFound -->|"No"| End(["No Action Required"])
    CollisionFound -->|"Yes"| EvalHolidayType{"Classification of Declared Holiday"}

    %% Full-Day Holiday
    EvalHolidayType -->|"Full-Day Declared Holiday"| FullDayRestore["Cancel Leave Deduction for that Calendar Day:<br/>- Automatically restore 1.0 Day Credit to Employee Ledger<br/>- Ledger Notation: 'Restored - Declared Holiday [Holiday Name]'<br/>- DTR Status: Holiday (Paid)"] --> NotifyEmp

    %% Half-Day Holiday
    EvalHolidayType -->|"Half-Day Declared Holiday (e.g., Work Suspended at 12:00 PM)"| HalfDayLogic["Execute CGB Half-Day Restoration Business Rule:<br/>1. Restore ENTIRE 1.0 Day Credit to Employee Leave Ledger<br/>2. Flag DTR with Tardiness / Undertime corresponding to the unworked half-day session not covered by suspension"] --> UpdateDTR["Transmit Half-Day Undertime Flag to DTR / Leave Ledger (Red Font)"] --> NotifyEmp

    NotifyEmp["Notify Employee & AO of Credit Adjustments"] --> End
```

---

### Process 13: Leave Ledger Maintenance, Tardiness Deduction & Manual Override
*   **System Box:** `1.3.1` & `1.3.2`
*   **Trigger:** Monthly DTR consolidation or manual administrative adjustment.
*   **Actors:** HR Admin (CHRMO), Department AO (Viewer), Employee (Viewer).

```mermaid
flowchart TD
    Start(["Monthly DTR Consolidation Received by CHRMO"]) --> LoopEmp["Process Employee Monthly Attendance Record"]
    LoopEmp --> CheckTardiness{"Did Employee Incur Tardiness or Undertime?"}

    CheckTardiness -->|"No"| ProceedAccrual["Proceed to Standard Monthly Accrual"]
    CheckTardiness -->|"Yes"| CSCConversion["Convert Hours and Minutes per CSC Table IV:<br/>Hours * 0.125 + Minutes * 0.002083"]

    CSCConversion --> DeductVL{"Check Vacation Leave (VL) Balance"}
    DeductVL -->|"VL Balance >= Deduction"| ApplyVLDeduct["Deduct Tardiness/Undertime from VL Balance<br/>Render Ledger Entry in RED FONT"]
    DeductVL -->|"VL Balance < Deduction"| ExhaustVL["Deduct Available VL to 0.000<br/>Convert Remaining Excess to Leave Without Pay (LWOP)<br/>Render LWOP in RED FONT"]

    ApplyVLDeduct & ExhaustVL --> CheckManualOverride{"Does HR Admin Need to Execute Manual Override?"}
    CheckManualOverride -->|"No"| FinalizeMonth["Commit Ledger Card Updates"]
    CheckManualOverride -->|"Yes"| AuthOverride["HR Admin Enters Administrative Correction:<br/>- Corrected Credit Value<br/>- Mandatory Upload of Supporting Memo / Office Order<br/>- Immutable Audit Log Record Created"] --> FinalizeMonth

    FinalizeMonth --> NextEmp{"More Employees?"}
    NextEmp -->|"Yes"| LoopEmp
    NextEmp -->|"No"| End(["Ledger Maintenance Completed"])
```

---

### Process 14: Compensatory Overtime Credits (COC/CTO) Lifecycle (Plantilla / Casual)
*   **System Box:** `1.3.3` (Track A)
*   **Trigger:** Completion of authorized overtime work under CSC-DBM Joint Circular No. 1, s. 2006.
*   **Actors:** Employee, Department Head, CHRMO.

```mermaid
flowchart TD
    Start(["Overtime Assignment Completed"]) --> SubmitCOCApp["Department Submits COC Application with Approved DTR & Accomplishment Report"]
    SubmitCOCApp --> CHRMAudit["CHRMO Computes Overtime Credits:<br/>- Regular Working Day Overtime: Hours * 1.0<br/>- Weekend / Holiday Overtime: Hours * 1.5"]
    CHRMAudit --> CheckCap{"Check Cumulative Unused COC Balance"}
    CheckCap -->|"Exceeds 120 Hours (15 Days)"| CapAt120["Cap Credit at 120 Hours Maximum Statutory Ceiling"]
    CheckCap -->|"<= 120 Hours"| CreditCOC["Credit Exact Computed Hours to COC Ledger"]

    CapAt120 & CreditCOC --> SetExpiration["Set Expiration Date: Exactly 1 Year from Date of Earning"]
    SetExpiration --> AvailCTO{"Employee Files Application for Compensatory Time-Off (CTO)?"}
    AvailCTO -->|"No"| CheckExpiry{"Has 1 Year Elapsed?"}
    CheckExpiry -->|"Yes"| AutoExpire["Forfeit Unused COC Credits from Ledger"] --> End(["Credits Forfeited"])
    CheckExpiry -->|"No"| KeepActive["Keep Credits Active"] --> AvailCTO

    AvailCTO -->|"Yes"| FileCTO["Submit CTO Application (Max 5 consecutive days/availment)"]
    FileCTO --> ApproveCTO["Dept Head & Mayor Approval"]
    ApproveCTO --> DeductCOC["Deduct Utilized Hours from COC Ledger (FIFO: Oldest Credits First)"] --> End(["CTO Availment Completed"])
```

---

### Process 15: Overtime & Time Offset (TO) Lifecycle (Non-Govt: COS / JO)
*   **System Box:** `1.3.3` (Track B)
*   **Trigger:** COS/JO personnel rendering authorized overtime for urgent municipal projects.
*   **Actors:** COS/JO Personnel, Project Supervisor, Department Head, CHRMO.

```mermaid
flowchart TD
    Start(["Project Overtime Required for COS / JO Personnel"]) --> FileOTForm["File Overtime Request Form (forms__overtime-request-form.docx)<br/>Signed by Project Supervisor & Dept Head"]
    FileOTForm --> ExecuteWork["Render Authorized Project Overtime"]
    ExecuteWork --> CertifyCETO["CHRMO Validates Attendance & Issues Certificate of Earned Time-Off (CETO)"]
    CertifyCETO --> PostETOLedger["Post Earned Offset Hours to Earned Time-Off Ledger (reports__earned-time-off-ledger.docx)"]

    PostETOLedger --> AbsenceOffset{"COS / JO Incurs Absence or Undertimes?"}
    AbsenceOffset -->|"Yes"| FileOffset["Submit Time Offset Application (forms__time-offset-application.docx)"]
    FileOffset --> VerifyETO{"Check Earned Time-Off Balance"}
    VerifyETO -->|"Insufficient"| SalaryDeduct["Absence Subject to Pro-Rata Daily Wage Deduction"] --> End(["Processed via Payroll"])
    VerifyETO -->|"Sufficient"| ApproveOffset["Dept Head & CHRMO Approve Time Offset"]
    ApproveOffset --> DeductETO["Deduct Offset Hours from Earned Time-Off Ledger<br/>Prevent Wage Deduction"] --> End(["Offset Applied Successfully"])
```

---

### Process 16: Regulatory Compliance Reporting (MRATU & SRATU)
*   **System Box:** `1.4.1`
*   **Trigger:** Monthly payroll cutoff and HR compliance calendar.
*   **Actors:** Department Admin Officer, Department Head, CHRMO, City Accounting/Payroll.

```mermaid
flowchart TD
    Start(["Monthly Attendance Cutoff Reached"]) --> CompileDTR["Compile All Validated Department DTRs & Leave Ledgers"]
    CompileDTR --> GenMRATU["Generate Monthly Report on Absence, Tardiness & Undertime (MRATU)"]

    subgraph MRATUDualSheet ["Dual-Sheet Architecture"]
        direction TB
        S1["Sheet 1: Regular MRATU<br/>(Plantilla Regular Personnel)"]
        S2["Sheet 2: Casual MRATU<br/>(Casual & Contractual Personnel)"]
    end

    GenMRATU --> MRATUDualSheet
    MRATUDualSheet --> GenSRATU["Generate Summary Report on Absences, Tardiness & Undertime (SRATU)<br/>Executive Departmental Summary"]

    GenSRATU --> SignReport["Department Head Certifies SRATU & MRATU"]
    SignReport --> TransmitCHRMO["Transmit Certified Reports to CHRMO"]
    TransmitCHRMO --> PayrollSync["System Synchronizes Deductions with Payroll Masterfile:<br/>- Direct salary deduction for LWOP<br/>- Direct salary deduction for excess tardiness"] --> End(["Monthly Compliance Finalized"])
```

---

### Process 17: Official HR Certifications Issuance
*   **System Box:** `1.4.2`
*   **Trigger:** Request by active or separated employee for official certification of credits.
*   **Actors:** Requesting Employee, Records Officer, CHRMO Head.

```mermaid
flowchart TD
    Start(["Employee Requests Official Certification"]) --> SelectCert{"Select Certification Type"}

    SelectCert -->|"Leave Credits (Plantilla/Casual)"| QueryCredits["Fetch Real-Time Balances from Leave Ledger Card"]
    QueryCredits --> GenEarnedCert["Generate Certificate of Earned Leave Credits<br/>(certificates__certificate-of-earned-leave.docx):<br/>- Inclusive Dates of Service<br/>- Total Accumulated VL Balance<br/>- Total Accumulated SL Balance<br/>- Purpose (Transfer / Clearance / Monetization)"]
    GenEarnedCert --> SignEarned["Signed by CHRMO Head"] --> ReleaseCert

    SelectCert -->|"Time-Off Credits (COS / JO)"| QueryETO["Fetch Approved Hours from Earned Time-Off Ledger"]
    QueryETO --> GenCETOCert["Generate Certificate of Earned Time-Off (CETO)<br/>(certificates__certificate-of-earned-time-off-(CETO).docx):<br/>- Project Assignment Reference<br/>- Approved Overtime Hours Earned<br/>- Remaining Available Offset Hours"]
    GenCETOCert --> SignCETO["Certified by Department Head & CHRMO Head"] --> ReleaseCert

    ReleaseCert(["Release Official Stamped Certificate to Employee"])
```

---

### Process 18: Operational Schedules & DTR Rectification Management
*   **System Box:** `1.4.3`
*   **Trigger:** Monthly shift scheduling or biometric device recording failure.
*   **Actors:** Department AO, Employee, Department Head, CHRMO.

```mermaid
flowchart TD
    Start(["Operational Schedule or Biometric Anomaly Trigger"]) --> Branch{"Action Type"}

    Branch -->|"Shift Scheduling"| LoadWorkSchedule["Load Work Schedule Master (reports__work-schedule.xlsx)"]
    LoadWorkSchedule --> AssignShifts["Assign Departmental Shifts, Flexitime Windows & Rotations"]
    AssignShifts --> PublishSchedule["Publish Schedule to DTR Attendance Engine"] --> End(["Roster Active"])

    Branch -->|"Biometric Punch Anomaly"| OpenRectification["Employee Initiates DTR Rectification Form<br/>(forms__dtr-rectification-form.xlsx)"]
    OpenRectification --> InputAnomaly["Specify Date, Missing Punch Type (In/Out), and Reason:<br/>- Biometric device offline / power interruption<br/>- Fieldwork / official business without mobile punch"]
    InputAnomaly --> AttachProof["Attach Supporting Evidence (e.g., Locator Slip, Office Pass)"]
    AttachProof --> DeptHeadVerify["Department Head Reviews & Recommends Rectification"]
    DeptHeadVerify --> CHRMOCommit["CHRMO Approves and Adjusts DTR Log Entry:<br/>- Corrects Missing Punch<br/>- Prevents Erroneous AWOL or Tardiness Flag in Ledger"] --> End(["Attendance Reconciled"])
```

---

### Process 19: Downstream Integration — Notice of Step Increment (NOSI) Postponement
*   **System Section:** `Section 6.1`
*   **Trigger:** Posting of Leave Without Pay (LWOP) into Employee Leave Ledger.
*   **Actors:** Automated Engine, HR Compensation & Benefits Section.

```mermaid
flowchart TD
    Start(["Posting of LWOP in Leave Ledger Card"]) --> QueryStepPeriod["Query Active 3-Year Step Increment Qualification Window"]
    QueryStepPeriod --> SumLWOP["Calculate Cumulative Days of LWOP within Step Window"]

    SumLWOP --> CheckThreshold{"Is Cumulative LWOP >= 15 Days?"}
    CheckThreshold -->|"No (< 15 Days)"| NoAdjustment["No Effect on Step Increment Date"] --> End(["Record Remains Unaltered"])
    CheckThreshold -->|"Yes (>= 15 Days)"| CalculatePostponement["Calculate NOSI Postponement Formula:<br/>Adjusted NOSI Date = Original NOSI Date + Total Cumulative Days of LWOP"]

    CalculatePostponement --> UpdateNOSIRecord["Update Employee HR Masterfile with Adjusted Step Effectivity Date"]
    UpdateNOSIRecord --> GenerateAlert["Generate Automated System Alert & Memo to HR Compensation & Benefits Section"]
    GenerateAlert --> LogAudit["Log Adjustment into Personnel Service Card Audit Trail"] --> End(["NOSI Postponement Finalized"])
```

---

### Process 20: Downstream Integration — 20-Day AWOL Detection & Dropping from Rolls Alert
*   **System Section:** `Section 6.2`
*   **Trigger:** Real-time logging of unauthorized absence in daily attendance.
*   **Actors:** Automated System Monitor, HR Admin, City Mayor.

```mermaid
flowchart TD
    Start(["Daily Attendance Processing Cycle"]) --> DetectUnauthorized["Identify Unauthorized Absence (No Approved Leave on Record)"]
    DetectUnauthorized --> AccumulateMonth["Calculate Total Cumulative AWOL Days in Current Calendar Month"]

    AccumulateMonth --> CheckAWOLThreshold{"Has Employee Accumulated >= 20 Days AWOL in Month?"}
    CheckAWOLThreshold -->|"No (< 20 Days)"| FlagDTR["Flag Attendance as Unauthorized Absence in DTR & Ledger"] --> End(["Normal Exception Processing"])
    CheckAWOLThreshold -->|"Yes (>= 20 Days AWOL)"| TriggerCriticalAlert["Trigger CRITICAL HIGH-PRIORITY SYSTEM ALERT to HR Admin"]

    TriggerCriticalAlert --> AutoDraftNotice["System Automatically Generates Official Documents:<br/>1. Return-to-Work Order / Show Cause Notice<br/>2. Draft Notice of Dropping from the Rolls (CSC Omnibus Rules Sec. 63)"]
    AutoDraftNotice --> AdminServe["HR Admin Reviews and Serves Notice to Employee's Registered Address"]
    AdminServe --> StartCountdown["System Initiates Statutory 5-Day Written Explanation Timer"]
    StartCountdown --> DropEvaluation{"Written Explanation Received within 5 Days?"}
    DropEvaluation -->|"Valid Justification Accepted"| ResolveAbsence["Convert Absence to Appropriate Leave Category"] --> End
    DropEvaluation -->|"No Reply or Unjustified"| SubmitMayorDrop["Transmits Recommendation for Dropping from the Rolls to City Mayor"] --> End(["Administrative Dropping Initiated"])
```

---

## 4. Verification and Cross-Reference Matrix

| System Flow v5 Box ID | Box Label | Mapped Process ID | Key Legal / Template Artifact |
| :--- | :--- | :--- | :--- |
| **1.1.1 & 1.1.1.1** | Different Types of Leave & Requirements | **Process 1** | CS Form No. 6 (Item 6.A/6.B), Omnibus Rules |
| **1.1.2.1 - 1.1.2.4** | Actual Leave Credits (Single Pane View) | **Process 2** | `reports__leave-ledger.xlsx`, Single-Pane UI |
| **1.1.2.5.1 (Auto)** | Automated Leave Crediting | **Process 3, 4** | CSC Tables I–III, RA 11210, RA 9710 |
| **1.1.2.5.1 (Manual)**| Manual Calamity Leave Crediting | **Process 5** | CSC MC 16, s. 2012, Calamity Declaration |
| **1.2.1 & 1.2.2.1** | Input Leave Details & Late Filing | **Process 6** | `forms__application-for-leave-form.xlsx` |
| **1.2.2.2** | Compliance & 5-Tier Approval Chain | **Process 7** | CS Form 6 (Item 7.A–7.D), CGB Delegation Orders |
| **1.2.2 (Commutation)**| Monetization & Terminal Leave Benefit | **Process 8, 9** | DBM BC 2016-2, Clearance Form |
| **1.2.3 & 1.2.3.1** | Modification of Approved Leave | **Process 10, 11, 12** | Admin Recall Memo, Holiday Restoration Engine |
| **1.3.1 & 1.3.2** | Leave Credits & Ledger Management | **Process 13** | `reports__leave-ledger.xlsx`, CSC Table IV |
| **1.3.3 (Track A)** | Compensatory Overtime Credits (COC/CTO) | **Process 14** | `forms__compensatory-time-off.docx`, CSC-DBM JC 1 |
| **1.3.3 (Track B)** | Earned Time-Off (ETO) for COS/JO | **Process 15** | `certificates__certificate-of-earned-time-off-(CETO).docx`, `reports__earned-time-off-ledger.docx` |
| **1.4.1** | Regulatory Compliance Reports | **Process 16** | `reports__monthly-report-on-absence-tardiness-undertime-(MRATU).xlsx`, `reports__summary-report-on-absences-tardiness-undertime-(SRATU).docx` |
| **1.4.2** | Official HR Certifications | **Process 17** | `certificates__certificate-of-earned-leave.docx`, CETO |
| **1.4.3** | Operational Schedules & Rectification | **Process 18** | `reports__work-schedule.xlsx`, `forms__dtr-rectification-form.xlsx` |
| **Integration 6.1** | Step Increment Postponement | **Process 19** | CSC-DBM JC on NOSI, Service Record Sync |
| **Integration 6.2** | 20-Day AWOL Automated Alert | **Process 20** | CSC MC 13, s. 2007, Dropping from the Rolls Notice |
