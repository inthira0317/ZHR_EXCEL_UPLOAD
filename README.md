# ZHR_EXCEL_UPLOAD
21-11-2026- Excel Upload Program in SAP ABAP to process employee Compensatory Off availability records, map Excel data to a custom database table, assign default Infotype 2006, and perform bulk database updates.

# SAP ABAP – Excel Upload Program for Compensatory Off Availability

## Project Overview

**Program Name:** `ZHR_EXCEL_UPLOAD`  
**Module:** SAP HCM – Human Resources  
**Technology:** SAP ABAP  
**Object Type:** Executable Report  
**Database Table:** `ZHR_ESS_COFF_AVL`

This project implements an Excel upload utility using SAP ABAP to upload employee Compensatory Off (COFF) availability details into a custom SAP database table.

The program reads employee-related information from an Excel spreadsheet, converts the spreadsheet data into an internal table, maps the uploaded values to the custom database table structure, and saves the records into the SAP database.

## Business Requirement

The HR team maintains Compensatory Off availability information in Excel spreadsheets. Manually entering each employee's details into SAP can be time-consuming.

To simplify this process, an ABAP report was developed to:

- Upload employee COFF availability details from Excel.
- Convert Excel records into an ABAP internal table.
- Assign the default Infotype value `2006`.
- Map Excel columns to the corresponding database fields.
- Insert or update records in the custom SAP table.
- Display the uploaded records for verification.

## Technical Details

| Component | Description |
|---|---|
| ABAP Report | `ZHR_EXCEL_UPLOAD` |
| Database Table | `ZHR_ESS_COFF_AVL` |
| Excel Conversion FM | `TEXT_CONVERT_XLS_TO_SAP` |
| File Selection FM | `F4_FILENAME` |
| Internal Table | `GT_FINAL` |
| Database Internal Table | `GT_AVL` |
| Database Operation | `MODIFY ... FROM TABLE` |
| Output | `CL_DEMO_OUTPUT=>DISPLAY` |

## Selection Screen

The report provides a selection screen with:

- Radio button options for upload processing.
- Excel file selection parameter.
- F4 help for browsing and selecting the Excel file.

## Excel Input Structure

The Excel file contains six columns.

| Excel Column | SAP Field | Description |
|---|---|---|
| COL1 | REQ_ID | Request ID |
| COL2 | ZDATE | Request Date |
| COL3 | NAME | Employee Name |
| COL4 | PERNR | Personnel Number |
| COL5 | SUBTY | Subtype |
| COL6 | AVL_DATE | Availed Date |

**Default Field Mapping:**

- `INFTY = '2006'` – Absence Infotype.

## Processing Logic

### 1. Excel File Selection

The `F4_FILENAME` function module provides file selection help to choose the Excel file from the local system.

### 2. Excel Data Conversion

The function module `TEXT_CONVERT_XLS_TO_SAP` converts Excel spreadsheet records into the internal table `GT_FINAL`.

The first row is treated as the header using `I_LINE_HEADER = 'X'`.

### 3. Internal Table Processing

The uploaded records are processed using a `LOOP AT` statement.

Each Excel column is mapped to its corresponding SAP database field.

### 4. Default Value Assignment

The Infotype field is assigned a default value:

`GS_AVL-INFTY = '2006'.`

This avoids requiring the Infotype value in the Excel file.

### 5. Database Update

The mapped records are appended to `GT_AVL`.

The following statement updates the custom database table:

`MODIFY ZHR_ESS_COFF_AVL FROM TABLE GT_AVL.`

`COMMIT WORK` is executed to save the database changes.

### 6. Output Display

The uploaded records are displayed using:

`CL_DEMO_OUTPUT=>DISPLAY( GT_AVL ).`

## ABAP Concepts Used

- Executable Reports
- Selection Screen Programming
- Radio Buttons
- F4 Help
- Function Modules
- Excel File Upload
- Internal Tables and Work Areas
- LOOP AT and APPEND
- Structure-to-Structure Field Mapping
- Database Table Operations
- COMMIT WORK
- Exception Handling
- ABAP Class `CL_DEMO_OUTPUT`

## Execution Flow

Excel File Selection  
↓  
Excel Data Conversion  
↓  
Internal Table `GT_FINAL`  
↓  
Loop Through Uploaded Records  
↓  
Field Mapping  
↓  
Assign Default Infotype 2006  
↓  
Append Records to `GT_AVL`  
↓  
Update Custom Database Table  
↓  
Display Uploaded Records

## Key Learning Outcomes

- Implemented Excel upload functionality using a standard SAP function module.
- Gained practical experience in processing external data in ABAP.
- Applied internal table operations for bulk record processing.
- Implemented field mapping between Excel data and custom SAP table fields.
- Used database operations to update custom SAP tables.
- Worked with SAP HCM Infotype 2006.

## Author

**SAP ABAP Developer**

GitHub: [github.com/inthira0317](https://github.com/inthira0317)

LinkedIn: [linkedin.com/in/bminthira](https://linkedin.com/in/bminthira)
