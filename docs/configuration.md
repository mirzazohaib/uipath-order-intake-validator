# Configuration Reference

This document describes the configuration values used by the project.

The Dispatcher stores its runtime configuration in:

```text
config/Config.xlsx
```

During initialization, the configuration is loaded into a DataTable and then converted into a dictionary for fast runtime lookups.

---

# Configuration Values

| Setting           | Type                   | Used By             | Description                                                  | Status  |
| ----------------- | ---------------------- | ------------------- | ------------------------------------------------------------ | :-----: |
| ComponentName     | String                 | Dispatcher          | Component name used in log messages.                         |   ✅    |
| Environment       | String                 | Dispatcher          | Environment identifier (for example DEV, TEST, PROD).        |   ✅    |
| QueueName         | String                 | Dispatcher          | Orchestrator Queue used when creating queue items.           |   ✅    |
| InputFilePath     | Relative Path          | Dispatcher          | Relative path to the source Excel workbook.                  |   ✅    |
| DefaultPriority   | String                 | Performer (planned) | Default priority when none is supplied.                      | Planned |
| MinimumQuantity   | Integer                | Performer (planned) | Minimum valid order quantity.                                | Planned |
| MinimumOrderValue | Decimal                | Performer (planned) | Minimum valid order value.                                   | Planned |
| ValidCountries    | Comma-separated String | Performer (planned) | List of supported countries used during business validation. | Planned |

---

# Dispatcher Configuration Flow

```text
Config.xlsx
      │
      ▼
Read Range
      │
      ▼
configDt (DataTable)
      │
      ▼
Dictionary(Of String, String)
      │
      ▼
Dispatcher
```

The Dispatcher currently reads these settings from the configuration dictionary:

- ComponentName
- Environment
- QueueName
- InputFilePath

These values are loaded once during initialization and reused throughout the workflow.

---

# Design Principles

The project follows these configuration principles:

- Keep runtime configuration outside the workflow.
- Read configuration once during startup.
- Store configuration in a dictionary for fast lookups.
- Use relative paths to keep the project portable.
- Separate runtime configuration from business processing logic.

---

# Future Configuration

The following settings are reserved for the Performer implementation:

- DefaultPriority
- MinimumQuantity
- MinimumOrderValue
- ValidCountries

These settings will be used when business validation is moved from the standalone validator into the queue-processing Performer.
