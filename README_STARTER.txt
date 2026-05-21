# UiPath Invoice Validation Bot - Starter Files

This File contains the starter input files for the UiPath RPA portfolio project.

## Folders

- `data/` contains the Excel input file: `invoices.xlsx`
- `invoices/` contains dummy PDF invoice files
- `approved/`, `review/`, `rejected/` are output folders for the bot
- `reports/` is where the bot will create its final report
- `screenshots/` can be used later for README screenshots

## Important test case

The Excel file contains a row for `missing-invoice.pdf`, but this PDF is intentionally not included.
This is used to test error handling in UiPath.

## Business rules for the bot

- Known supplier + valid amount + file exists -> APPROVED
- Unknown supplier -> REVIEW
- Amount <= 0 -> REJECTED
- Amount > 1000 -> REVIEW
- Missing PDF file -> REJECTED
