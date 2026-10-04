# Solution Architecture

This document describes the current solution architecture and the planned evolution of the project.

---

# Version 1 – ValidatorV1

A standalone Excel-based validation workflow.

```text
sample_orders.xlsx
        │
        ▼
   ValidatorV1
        │
        ├── validated_orders.xlsx
        ├── exceptions.xlsx
        └── processing_summary.xlsx
```

### Responsibilities

- Read order data from Excel.
- Apply business validation rules.
- Separate valid and exception records.
- Generate Excel output files.
- Produce a processing summary.

---

# Version 2 – Dispatcher

The Dispatcher separates work creation from work processing.

```text
                 Config.xlsx
                      │
                      ▼
           Configuration Loader
                      │
                      ▼
   Dictionary(Of String, String)
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
 Input File Path              Queue Name
        │                           │
        └─────────────┬─────────────┘
                      ▼
              sample_orders.xlsx
                      │
                      ▼
                 Dispatcher
                      │
                      ▼
           Orchestrator Queue
```

### Current Responsibilities

- Load shared configuration from `Config.xlsx`.
- Build a configuration dictionary during initialization.
- Read the input file path from configuration.
- Read the Orchestrator queue name from configuration.
- Read incoming orders from Excel.
- Perform structural validation.
- Create queue items in Orchestrator.
- Produce standardized log messages using configurable component and environment information.

---

# Planned Version – Dispatcher and Performer

The next stage introduces a Performer based on the UiPath REFramework.

```text
                Config.xlsx
                     │
                     ▼
              Shared Configuration
                     │
      ┌──────────────┴──────────────┐
      │                             │
      ▼                             ▼
 Dispatcher                   Performer
      │                             │
      ▼                             ▼
Orchestrator Queue       Transaction Processing
                                    │
                                    ▼
                            Business Result
```

### Dispatcher Responsibilities

- Read source data.
- Perform structural validation.
- Create queue transactions.

### Performer Responsibilities

- Retrieve queue transactions.
- Perform business validation.
- Process each transaction.
- Handle Business Exceptions.
- Handle System Exceptions.
- Update transaction status.
- Produce processing results.

---

# Design Principles

The project follows these design principles:

- Separate work creation from work processing.
- Keep business configuration outside the workflow where practical.
- Read configuration once during initialization.
- Store configuration in a dictionary for fast runtime lookups.
- Keep logging consistent across workflows.
- Build the solution incrementally and verify each feature before introducing the next.
