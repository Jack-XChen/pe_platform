# Business Requirement Document (BRD)
## SAT Inspection Automation System

---

## 1. Background

SAT (Site Acceptance Test) equipment qualification records are currently prepared manually using Microsoft Excel.

Inspection engineers manually copy data, insert images, and repeatedly format tables to generate similar reports on a daily basis. Daily inspection tasks are tracked separately from reporting documents, resulting in limited visibility of progress and potential inconsistencies.

Image evidence is stored independently from report files, increasing preparation time and introducing risk of incomplete documentation.

---

## 2. Problem Statement

The current SAT reporting workflow presents the following challenges:

- Manual report preparation requires significant repetitive formatting effort.
- Lack of centralized task tracking reduces visibility of project progress.
- Image evidence management is disconnected from reporting structure.
- Resource and material preparation is not proactively aligned with scheduled inspection tasks.
- Report generation is time-consuming and may delay project delivery.

---

## 3. Objectives

The objectives of this project are to:

1. Provide real-time visualization of SAT report progress, including:
   - Number of completed inspection items
   - Total number of inspection items
   - Estimated completion date

2. Automatically generate daily inspection task prompts based on the original SAT inspection schedule, while allowing users to:
   - Complete inspection items in advance
   - Manually select and mark inspection items as completed

3. Standardize inspection data entry by generating structured input forms derived from predefined SAT inspection templates.

4. Support direct image attachment from mobile devices as inspection evidence.

5. Automatically generate a complete SAT report in Excel format, including all required fields and embedded image evidence in accordance with company reporting standards.

---

## 4. Business Value

Implementation of the SAT Inspection Automation System is expected to deliver the following business benefits:

1. **Reduced Project Duration**  
   SAT projects typically require 3 to 5 weeks depending on equipment complexity.  
   The automation of task planning, data entry, and report generation is expected to reduce overall project duration by approximately two weeks.

2. **Improved Task Planning and Resource Preparation**  
   Early visibility of scheduled inspection tasks enables proactive preparation of required materials and test equipment, reducing avoidable delays.

3. **Increased Documentation Efficiency**  
   Automated data consolidation and embedded image handling reduce manual formatting and repetitive reporting effort.

4. **Enhanced Progress Visibility**  
   Real-time tracking of completed versus total inspection items improves transparency for project management.

5. **Improved Delivery Predictability**  
   Structured workflow and centralized tracking reduce the risk of schedule overruns and improve on-time SAT report delivery.

---

## 5. Success Criteria

The project shall be considered successful if the following conditions are met:

1. The average SAT project duration is reduced by approximately two weeks compared to the current manual process.

2. Daily inspection tasks are automatically generated upon user login based on the SAT inspection schedule.

3. The system generates SAT Excel reports with correct structure and formatting, requiring no mandatory post-generation formatting adjustments.

4. 100% of required inspection images are automatically embedded in the exported Excel report.

5. Users retain the ability to manually adjust task completion status and report data when necessary.

---

## 6. Scope Definition

### 6.1 In Scope (v1.0)

1. Daily task generation and progress tracking.
2. Visualization of SAT progress metrics.
3. Structured inspection data entry.
4. CSV import functionality.
5. Image evidence upload and management.
6. Automatic Excel report generation with fixed columns.
7. Embedded image handling within Excel reports.
8. Basic multi-user support suitable for internal deployment.
9. Data storage and report regeneration capability.

### 6.2 Out of Scope (v1.0)

- OCR-based data extraction from images.
- Electronic signature functionality.
- Formal approval workflow process.
- Regulatory compliance audit tracking.
- ERP or third-party system integration.

---

## 7. Constraints & Assumptions

### 7.1 Constraints

- The Excel report format shall follow fixed-column standards mandated by company reporting requirements.
- Required inspection images shall be embedded directly into the Excel report.
- The system shall be designed with modular separation between task tracking, data entry, image management, and report generation to support future extensibility.

### 7.2 Assumptions

- Users will access the system via standard web browsers (desktop and mobile).
- SAT inspection templates remain stable during v1.0 implementation.
- Image uploads are provided manually by users as inspection evidence.

---

## 8. Stakeholders

Although the current organizational structure involves a single operator, responsibilities can be logically categorized as:

1. **Inspection Operator** – Executes SAT inspections and records inspection data.
2. **Project Tracking Owner** – Monitors SAT progress and delivery timeline.
3. **Report Owner** – Validates and delivers the final SAT report.

In the current structure, these responsibilities are handled by the same individual.

---

## 9. Risk Assessment

The following risks have been identified:

1. **File Size Risk**  
   Embedding images directly into Excel reports may increase file size and affect performance.

2. **Data Consistency Risk**  
   CSV import functionality may introduce inconsistent formatting or incomplete data.

3. **Template Change Risk**  
   Future changes to SAT inspection templates may require system updates.

4. **User Dependency Risk**  
   With a single primary operator, process continuity depends on consistent system usage.

---

## 10. Deployment Considerations

1. The system shall be deployable on a company-managed server environment.
2. Data shall be stored in a centralized database.
3. Image storage shall follow structured directory management.
4. Backup and data recovery procedures shall be considered prior to production deployment.

---

## 11. Future Scalability Vision

Although initially designed for internal use, the system architecture should support:

- Role-based access control
- Multi-user expansion
- Approval workflow integration
- Integration with future QA or ERP systems
- Advanced reporting and analytics capabilities

---
