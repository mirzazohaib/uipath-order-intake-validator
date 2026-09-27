# RPA Order Intake Validator

A UiPath portfolio project that validates order-intake data from Excel, separates valid rows from business exceptions, and creates a processing summary.

It is built to demonstrate UiPath/RPA fundamentals. The scope is intentionally small, but it covers the parts that matter in real automation work: reading input data, applying business rules, handling exception rows, writing outputs, logging the run, and documenting the process clearly.

## What the automation does

The bot reads `input/sample_orders.xlsx`, checks each order row, and creates three output files:

- `output/validated_orders.xlsx` for rows that pass all validation rules
- `output/exceptions.xlsx` for rows that fail one or more validation rules
- `output/processing_summary.xlsx` with total, valid, and exception counts

The current version also clears old output sheets before writing new data, uses relative file paths, logs key processing steps, and has top-level error handling.

## Demonstrated capabilities

- UiPath Studio workflow design
- Excel automation with `Use Excel File`, `Read Range`, `Clear Range`, and `Write DataTable to Excel`
- DataTable creation and row-by-row processing
- Business-rule validation with independent checks
- Multiple exception reasons accumulated for the same row
- Basic logging with `Log Message`
- Top-level `Try Catch` error handling
- Relative project paths suitable for GitHub
- Clean input, output, and documentation folder structure

## Workflow overview

The workflow is documented with Mermaid diagrams in:

[View process diagrams](docs/diagrams.md)

The diagrams show:

- End-to-end process flow
- Validation decision logic
- Output generation flow

## Repository structure

Current project structure:

```text
uipath-order-intake-validator/
│
├── README.md
├── .gitignore
│
├── docs/
│   └── diagrams.md
│
├── input/
│   └── sample_orders.xlsx
│
├── output/
│   ├── exceptions.xlsx
│   ├── processing_summary.xlsx
│   └── validated_orders.xlsx
│
└── UiPath/
    └── OrderIntakeValidator/
        ├── Main.xaml
        ├── project.json
        ├── project.uiproj
        ├── entry-points.json
        ├── AGENTS.md
        ├── CLAUDE.md
        ├── .entities/
        ├── .objects/
        ├── .project/
        ├── .templates/
        └── .tmh/
```

## Input file

Input file:

```text
input/sample_orders.xlsx
```

Expected columns:

| Column          | Purpose                      |
| --------------- | ---------------------------- |
| `OrderId`       | Unique order identifier      |
| `CustomerName`  | Customer or company name     |
| `CustomerEmail` | Customer email address       |
| `Country`       | Order country                |
| `Product`       | Product or service requested |
| `Quantity`      | Requested quantity           |
| `OrderValue`    | Order value                  |
| `RequestDate`   | Request date                 |
| `Priority`      | Priority value               |

The sample file includes valid rows and deliberately invalid rows for testing missing email, unsupported country, zero quantity, negative order value, lowercase country input, and multiple errors in one row.

## Validation rules

| Field           | Rule                                           | Exception reason            |
| --------------- | ---------------------------------------------- | --------------------------- |
| `CustomerEmail` | Must not be empty and must contain `@`         | `Invalid or missing email;` |
| `Country`       | Must be Finland, Estonia, Latvia, or Lithuania | `Country not supported;`    |
| `Quantity`      | Must be numeric and greater than 0             | `Invalid quantity;`         |
| `OrderValue`    | Must be numeric and greater than 0             | `Invalid order value;`      |
| `Priority`      | If empty, set to `Normal`                      | No exception                |

Country values are trimmed and converted to uppercase before validation, so values such as `finland`, `FINLAND`, and `Finland` are accepted.

The validation checks are independent. If one row fails several checks, all exception reasons are captured. For example:

```text
Invalid or missing email; Invalid quantity; Invalid order value;
```

## Test result

Using the current sample file, the summary output is:

| Metric           | Value |
| ---------------- | ----: |
| Total Orders     |     9 |
| Valid Orders     |     4 |
| Exception Orders |     5 |

Valid orders:

| OrderId  | CustomerName     | Country   | Quantity | OrderValue | Priority | Status |
| -------- | ---------------- | --------- | -------: | ---------: | -------- | ------ |
| ORD-1001 | Nordic Fuel Oy   | Finland   |        5 |       1250 | High     | Valid  |
| ORD-1002 | Baltic Logistics | Estonia   |        3 |        900 | Normal   | Valid  |
| ORD-1006 | Missing Priority | Lithuania |        4 |       1100 | Normal   | Valid  |
| ORD-1008 | Valid Baltic     | Latvia    |        6 |       1800 | High     | Valid  |

Exception rows:

| OrderId  | Reason                                                           |
| -------- | ---------------------------------------------------------------- |
| ORD-1003 | Invalid or missing email;                                        |
| ORD-1004 | Country not supported;                                           |
| ORD-1005 | Invalid quantity;                                                |
| ORD-1007 | Invalid order value;                                             |
| ORD-1009 | Invalid or missing email; Invalid quantity; Invalid order value; |

## How to run

1. Clone or download the repository.
2. Open the UiPath project:

```text
UiPath/OrderIntakeValidator/project.uiproj
```

3. Confirm that the folder structure is unchanged:

```text
input/sample_orders.xlsx
output/
UiPath/OrderIntakeValidator/
```

4. Run `Main.xaml` from UiPath Studio.
5. Check the output folder after the run:

```text
output/validated_orders.xlsx
output/exceptions.xlsx
output/processing_summary.xlsx
```

## Path handling

The workflow uses relative paths from the UiPath project folder. The expected structure is:

```text
uipath-order-intake-validator/
├── input/
├── output/
└── UiPath/
    └── OrderIntakeValidator/
        └── Main.xaml
```

The workflow refers to input and output files through paths such as:

```text
..\..\input\sample_orders.xlsx
..\..\output\validated_orders.xlsx
..\..\output\exceptions.xlsx
..\..\output\processing_summary.xlsx
```

## Error handling and logging

The automation has a top-level `Try Catch`. If an unexpected runtime error occurs, the Catch block logs the failure message.

The workflow also logs key milestones:

- input file loaded and row count found
- processing completed with total, valid, and exception counts
- output files created successfully

This is basic error handling, not a full production support model.

## Known limitations

- The project uses Excel files as the input and output layer.
- Error handling is basic. A production version should add more specific Try/Catch blocks for missing files, locked files, missing columns, and invalid workbook structure.
- Validation rules are hardcoded in the workflow.
- The project does not use Orchestrator Queues yet.
- The project is a demo/learning portfolio automation, not a production-grade RPA package.

## Possible next improvements

- Move file paths and supported countries to a config file.
- Add column-existence validation before row processing.
- Add Orchestrator Queues with a Dispatcher/Performer pattern.
- Add REFramework structure for transaction processing.
- Add separate logs for business exceptions and system exceptions.
- Add automated test data variations.
- Add an email notification after output files are created.

## Status

Current version: interview-ready demo project.

The bot demonstrates core UiPath/RPA concepts clearly and leaves larger production topics, such as Orchestrator Queues and REFramework, as planned next steps.
