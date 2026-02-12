# Software Requirements Specification (SRS)
## SAT Inspection Automation System

### Document Control
- Version: v0.1
- Date: 2026-02-11
- Author: <Your Name>
- Derived From: BRD v0.1

---

## 1. Purpose
This document specifies the functional and non-functional requirements for the SAT Inspection Automation System.
The system standardizes SAT inspection workflow, generates daily tasks upon login, manages image evidence, and produces Excel SAT reports with fixed columns and embedded images.

---

## 2. Scope

### 2.1 In Scope (v1.0)
- Multi-template SAT project setup (per base station).
- Daily task generation and progress visualization.
- Data entry via web forms and CSV import (with overwrite support).
- Image evidence upload (0–10 images per inspection item).
- Excel report generation with fixed columns and embedded images.
- Estimation of completion date using remaining workload + historical velocity.

### 2.2 Out of Scope (v1.0)
- OCR-based extraction from photos.
- Electronic signatures.
- Formal approval workflow.
- Integration with ERP/QA systems.

---

## 3. Definitions
- **SAT**: Site Acceptance Test.
- **Base Station**: A site/category that determines the inspection template.
- **Template**: The inspection structure for a base station; similar across machines within the same base station but not necessarily identical.
- **Inspection Item**: A single check/test step that must be completed and recorded.
- **Evidence**: Photos attached to an inspection item.
- **Velocity**: Historical completion rate (items/day) for a given base station or project.

---

## 4. Users and Roles
Although current operation may be single-user, the system shall support logical roles:
- **Operator**: performs inspections, inputs data, uploads images.
- **Report Owner**: generates/export final reports.
- **Admin (optional in v1.0)**: manages templates and system settings.

---

## 5. System Overview
The system consists of the following modules (logically separated for extensibility):
1. Template Management
2. Project & Schedule Management
3. Daily Task & Progress Dashboard
4. Data Entry (Forms + CSV Import)
5. Evidence (Image) Management
6. Excel Report Generator

---

## 6. Data Model Summary (High-Level)
The system shall represent at minimum:
- **BaseStationTemplate**
  - template_id, base_station_name, template_version, layout_rules
- **InspectionProject**
  - project_id, base_station_name, equipment_id, start_date, target_date (optional)
- **InspectionItem**
  - item_id, project_id, item_name, due_date, status, result_fields (typed)
- **EvidenceImage**
  - image_id, item_id, file_path, uploaded_at, uploader
- **ReportArtifact**
  - report_id, project_id, generated_at, generated_by, report_file_path, report_version

> Note: exact schema is defined in the System Design Doc; SRS only defines required entities/relationships.

---

## 7. Functional Requirements

### 7.1 Template Management

**FR-01 Template Definition**
- The system shall support multiple templates, where each base station can have its own template.
- Templates for different machines within the same base station shall be allowed to share common structure but may differ in specific items.

**FR-02 Template Versioning**
- The system shall allow templates to be versioned.
- A project shall reference the specific template version used at project creation time.

**FR-03 Template-Driven Layout Rules**
- The system shall store layout rules that determine how evidence images are embedded into Excel (e.g., placement, scaling, stacking).
- Layout rules shall be applied during report generation.

---

### 7.2 Project & Schedule

**FR-04 Project Creation**
- The system shall allow users to create an inspection project by selecting a base station template and providing equipment identifiers.

**FR-05 Item Schedule Generation**
- The system shall generate inspection items and their schedule from the selected template.
- Items may have due dates derived from template offsets or user-defined schedule.

---

### 7.3 Daily Tasks & Progress Dashboard

**FR-06 Auto Daily Task Generation (Login Trigger)**
- Upon user login, the system shall automatically generate the task list for the current date based on item due dates and status.

**FR-07 Manual Task Selection**
- The system shall allow users to manually select tasks to be completed for a given day regardless of due date.

**FR-08 Early Completion**
- The system shall allow inspection items to be completed before their scheduled due date.

**FR-09 Progress Visualization**
- The system shall display progress metrics including:
  - completed items count
  - total items count
  - completion percentage
  - estimated completion date

**FR-10 Estimated Completion Date Calculation**
- The system shall estimate completion date using:
  - remaining item count
  - historical completion velocity (items/day)
- If insufficient history exists, the system shall fall back to a default velocity configurable per base station.

---

### 7.4 Data Entry

**FR-11 Structured Data Entry Forms**
- The system shall provide template-driven forms for inspection result entry.
- Required fields shall be enforced based on template definitions.

**FR-12 Field Validation**
- The system shall validate required fields, data types (date/number/text), and allowed ranges where applicable.
- Invalid submissions shall be rejected with actionable error messages.

---

### 7.5 CSV Import

**FR-13 CSV Import**
- The system shall allow users to import inspection data from CSV.
- The system shall validate that CSV columns match the fixed-column definition and template mapping rules.

**FR-14 Overwrite Policy**
- CSV import shall support overwriting existing records.
- Overwrite behavior shall be explicit (e.g., by matching item identifiers or composite keys).
- The system shall provide an import summary:
  - created count
  - updated count
  - rejected rows with reasons

---

### 7.6 Evidence (Image) Management

**FR-15 Evidence Upload**
- The system shall allow users to upload image evidence from desktop or mobile devices.
- Supported formats shall include JPG and PNG.

**FR-16 Evidence Limits**
- Each inspection item shall allow 0 to 10 images.
- The system shall enforce the maximum image count per item.

**FR-17 Evidence-to-Item Binding**
- Each image shall be associated with exactly one inspection item.

---

### 7.7 Excel Report Generation

**FR-18 Fixed Column Excel Output**
- The system shall generate an Excel report with fixed column headers and fixed column order as mandated by company standards.

**FR-19 Embedded Image Requirement**
- The system shall embed required evidence images directly into the Excel workbook.

**FR-20 Template-Driven Evidence Layout**
- Image placement/formatting in Excel shall follow template layout rules (e.g., which column, scaling, multi-image arrangement).

**FR-21 One-Click Report Generation**
- The system shall allow generating the full SAT report for a project with a single action.

**FR-22 Manual Adjustments**
- The system shall allow manual adjustment of task status and report data prior to final export.
- Manual adjustments shall not break fixed column structure.

**FR-23 Regeneration**
- The system shall allow regenerating reports from stored data at any time.

---

## 8. Non-Functional Requirements

**NFR-01 Performance**
- Daily task generation shall complete within 3 seconds under normal load.
- Excel report generation shall complete within 60 seconds for:
  - up to 300 inspection items
  - up to 10 images per item
  (best-effort; may be hardware-dependent)

**NFR-02 Reliability**
- The system shall prevent data loss under normal operation.
- Failed report generation shall not corrupt stored inspection records.

**NFR-03 Compatibility**
- Generated Excel reports shall be compatible with Microsoft Excel 2016 or later.

**NFR-04 Maintainability (Modular Separation)**
- The system shall maintain logical separation between:
  - task scheduling
  - template management
  - evidence management
  - report generation
  to support future extension without major refactoring.

**NFR-05 Security (Baseline)**
- The system shall require authenticated access for data entry and report generation.
- Uploaded evidence files shall not be publicly accessible without authorization.

---

## 9. Acceptance Criteria (MVP Examples)

### AC-01 Login Task Generation
- Given a project with items due today, when a user logs in, the dashboard lists all due items and shows updated progress metrics.

### AC-02 CSV Overwrite
- Given existing item results, when a CSV import is performed with overwrite enabled, the system updates matched items and produces an import summary with updated counts.

### AC-03 Evidence Upload Limits
- For a single inspection item, uploading the 11th image is rejected with a clear error.

### AC-04 Excel Report with Embedded Evidence
- Generated Excel opens without errors in Excel 2016+.
- Evidence images are embedded and placed according to the template layout rules.
- Column headers and column order exactly match the fixed-column specification.

---

## 10. Open Items (To be finalized)
- Fixed column list (exact headers and order).
- Template layout rule schema (how to specify placement/stacking/scaling).
- Default velocity per base station for completion estimation.
- Max image file size and compression policy (recommended for server performance).

---
