# UiPath Invoice Validation & Filing Bot

A small UiPath RPA portfolio project that automates a realistic invoice validation process.

The bot reads invoice metadata from an Excel file, validates each invoice using business rules, checks whether the related PDF file exists, writes the processing result back to Excel, copies invoice files into status-based folders, and generates a final processing report.

This project was built as a beginner-to-intermediate UiPath portfolio project to demonstrate practical RPA skills.

---

## Project Goal

The goal of this project is to simulate a common business process:

> A company receives invoices from suppliers. A human normally checks the invoice data, validates the supplier and amount, verifies that the invoice file exists, and sorts the invoice into the correct processing folder.

This UiPath bot automates that process.

---

## What the Bot Does

The automation performs the following steps:

1. Opens an Excel file containing invoice data.
2. Loops through each invoice row.
3. Reads invoice fields such as invoice ID, supplier, amount, due date, and file name.
4. Validates each invoice using business rules.
5. Checks whether the related PDF invoice file exists.
6. Writes the result back to Excel:
   - Status
   - Comment
   - ProcessedAt timestamp
7. Copies the PDF file into the correct folder:
   - `approved`
   - `review`
   - `rejected`
8. Counts the processing results.
9. Generates a text report.
10. Opens the final report automatically.

---

## Business Rules

The bot uses the following validation rules:

| Rule | Result |
|---|---|
| Invoice PDF file is missing | REJECTED |
| Amount is less than or equal to 0 | REJECTED |
| Supplier is unknown | REVIEW |
| Amount is greater than 1000 | REVIEW |
| Supplier is known and amount is valid | APPROVED |

Known suppliers:

- Amazon Business
- Vodafone
- Dell
- Microsoft
- Metro

---

## Example Input

The input data is stored in:

```text
data/invoices.xlsx
```

Example rows:

| InvoiceId | Supplier | Amount | DueDate | FileName |
|---|---|---:|---|---|
| INV-001 | Amazon Business | 120.50 | 2026-06-01 | INV-001.pdf |
| INV-003 | Unknown Supplier | 800.00 | 2026-06-10 | INV-003.pdf |
| INV-004 | Dell | -50.00 | 2026-06-12 | INV-004.pdf |
| INV-008 | Vodafone | 150.00 | 2026-06-22 | missing-invoice.pdf |

---

## Example Output

After processing, the Excel file is updated with results like:

| InvoiceId | Supplier | Amount | Status | Comment |
|---|---|---:|---|---|
| INV-001 | Amazon Business | 120.50 | APPROVED | Invoice valid |
| INV-003 | Unknown Supplier | 800.00 | REVIEW | Unknown supplier |
| INV-004 | Dell | -50.00 | REJECTED | Amount is invalid |
| INV-008 | Vodafone | 150.00 | REJECTED | Invoice file missing |

The bot also creates a report like:

```text
Invoice Processing Report
Generated at: 2026-05-21 21:30:00

Total invoices: 8
Approved: 3
Review: 2
Rejected: 3
Missing files: 1
```

---

## Folder Structure

```text
UiPath-Invoice-Validation-Bot
│
├── InvoiceValidationBot
│   ├── Main.xaml
│   └── project.json
│
├── data
│   └── invoices.xlsx
│
├── invoices
│   ├── INV-001.pdf
│   ├── INV-002.pdf
│   ├── INV-003.pdf
│   ├── INV-004.pdf
│   ├── INV-005.pdf
│   ├── INV-006.pdf
│   └── INV-007.pdf
│
├── approved
├── review
├── rejected
├── reports
├── screenshots
├── .gitignore
└── README.md
```

---

## UiPath Concepts Demonstrated

This project demonstrates the following UiPath and RPA concepts:

- Excel automation
- Reading structured input data
- Row-by-row processing
- Variables
- Conditions with `If`
- Business rule validation
- File existence checks
- File copying
- Writing results back to Excel
- Logging
- Report generation
- Opening output files automatically
- Basic process documentation
- Git/GitHub version control

---

## Current Status

Implemented:

- Read invoice data from Excel
- Process each invoice row
- Validate invoice amount
- Validate supplier
- Check whether invoice PDF exists
- Write status, comment, and timestamp back to Excel
- Copy invoice files into approved, review, or rejected folders
- Count approved, review, rejected, and missing-file cases
- Generate a final text report
- Open the report automatically after execution

Planned improvements:

- Add structured error handling using `Try Catch`
- Improve logging for unexpected runtime errors
- Add screenshots to the README
- Add a short demo GIF or video


---

## Why This Project Is Relevant for RPA

Invoice processing is a common business process in companies. This project shows how RPA can automate repetitive manual work such as reading Excel data, validating business rules, handling files, updating records, and creating reports.


It demonstrates that RPA is not only about clicking buttons. A useful bot should follow a clear process:

```text
Input -> Validation -> Decision -> Action -> Output -> Report
```

---

## Difference Compared to API Workflow Automation

This UiPath project focuses on RPA automation:

- Interacting with Excel files
- Handling local folders and documents
- Applying business rules
- Simulating manual back-office work
- Producing user-readable output files

This is different from my n8n + LLM workflow automation project, which focuses more on:

- API-based automation
- Webhooks
- LLM integration
- PostgreSQL persistence
- Backend-style workflow orchestration

Together, both projects show two different automation approaches:

| Project | Automation Type |
|---|---|
| UiPath Invoice Validation Bot | RPA / desktop and file automation |
| n8n + LLM Support Workflow | API / workflow / AI automation |

---

## Tech Stack

- UiPath Studio
- Excel
- Windows file system
- Git
- GitHub

---

## How to Run the Project

1. Open the project in UiPath Studio.
2. Make sure the input file exists:

```text
data/invoices.xlsx
```

3. Make sure the invoice PDF files are inside:

```text
invoices
```

4. Run `Main.xaml`.
5. After execution, check:
   - Updated Excel file in `data`
   - Copied PDFs in `approved`, `review`, and `rejected`
   - Generated report in `reports`

---

## Notes

The file `missing-invoice.pdf` is intentionally not included. It is used to test the bot's missing-file validation rule.

The generated report files and copied invoice PDFs are runtime outputs and should not be committed to GitHub.

---

## Author

Ahmed Amine Kadri  
Computer Science Bachelor student  
Heinrich-Heine-Universität Düsseldorf
