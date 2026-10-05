# RPA Order Intake Validator

A UiPath portfolio project that demonstrates how an order-intake automation can evolve from a standalone Excel validation workflow into a queue-based Dispatcher architecture.

The project is developed incrementally to demonstrate practical UiPath development practices, including workflow design, Orchestrator Queues, configuration management, Git version control, and technical documentation.

---

# Project Overview

The repository currently contains two UiPath projects.

## ValidatorV1

A standalone workflow that:

- Reads order data from an Excel workbook.
- Applies business validation rules.
- Separates valid and exception records.
- Produces a processing summary.

## Dispatcher

A queue-based workflow that:

- Reads incoming orders from Excel.
- Performs structural validation.
- Creates Orchestrator Queue transactions.
- Loads runtime configuration from `Config.xlsx`.
- Uses standardized logging.

The Performer implementation using UiPath REFramework is planned as the next major development phase.

---

# Repository Structure

```text
uipath-order-intake-validator/
│
├── README.md
├── CHANGELOG.md
├── ROADMAP.md
├── .gitignore
│
├── config/
│   └── Config.xlsx
│
├── docs/
│   ├── architecture.md
│   ├── configuration.md
│   ├── decisions.md
│   ├── diagrams.md
│   └── milestones.md
│
├── input/
│   └── sample_orders.xlsx
│
├── output/
│   └── .gitkeep
│
└── UiPath/
    ├── Dispatcher/
    └── ValidatorV1/
```

---

# Features

## ValidatorV1

- Excel data processing
- Business-rule validation
- Exception reporting
- Processing summary generation
- Relative project paths
- Basic logging
- Top-level Try/Catch

## Dispatcher

- Orchestrator Queue integration
- Structural validation
- Shared configuration (`Config.xlsx`)
- Configuration dictionary
- Configuration-driven input file path
- Configuration-driven queue name
- Standardized logging
- Queue transaction creation

---

# Technologies

- UiPath Studio 26.x
- UiPath Orchestrator
- UiPath Excel Activities
- Git
- GitHub
- Mermaid

---

# Documentation

The repository documentation is organized by purpose to make it easier to understand the project architecture, configuration, development history, and planned evolution.

| Document                                         | Purpose                                             |
| ------------------------------------------------ | --------------------------------------------------- |
| [Solution Architecture](docs/architecture.md)    | High-level system design and project evolution.     |
| [Configuration Reference](docs/configuration.md) | Runtime configuration and configuration dictionary. |
| [Workflow Diagrams](docs/diagrams.md)            | Mermaid diagrams illustrating the workflows.        |
| [Design Decisions](docs/decisions.md)            | Important implementation decisions and rationale.   |
| [Project Milestones](docs/milestones.md)         | Major development milestones completed and planned. |
| [Roadmap](ROADMAP.md)                            | Planned future enhancements.                        |
| [Changelog](CHANGELOG.md)                        | Version history and notable changes.                |

---

# Workflow Overview

The solution is evolving toward a Dispatcher–Performer architecture.

Current workflow:

```text
Excel
   │
   ▼
Dispatcher
   │
   ▼
Orchestrator Queue
```

Planned workflow:

```text
Excel
   │
   ▼
Dispatcher
   │
   ▼
Orchestrator Queue
   │
   ▼
Performer (REFramework)
   │
   ▼
Business Processing
```

---

# Input Data

Current input workbook:

```text
input/sample_orders.xlsx
```

Expected columns:

| Column        | Description              |
| ------------- | ------------------------ |
| OrderId       | Unique order identifier  |
| CustomerName  | Customer or company name |
| CustomerEmail | Customer email address   |
| Country       | Order country            |
| Product       | Product or service       |
| Quantity      | Ordered quantity         |
| OrderValue    | Monetary value           |
| RequestDate   | Request date             |
| Priority      | Business priority        |

The sample workbook contains both valid and intentionally invalid records for testing validation logic.

---

# Configuration

The Dispatcher uses a shared configuration file:

```text
config/Config.xlsx
```

Currently implemented configuration:

- ComponentName
- Environment
- QueueName
- InputFilePath

Configuration is loaded once during initialization and stored in a dictionary for fast runtime lookups.

For additional details, see the [Configuration Reference](docs/configuration.md).

---

# How to Run

## ValidatorV1

Open:

```text
UiPath/ValidatorV1/project.uiproj
```

Run:

```text
Main.xaml
```

---

## Dispatcher

Open:

```text
UiPath/Dispatcher/project.uiproj
```

Verify that:

- `config/Config.xlsx` exists.
- `input/sample_orders.xlsx` exists.
- The configured Orchestrator Queue exists.

Run:

```text
Main.xaml
```

---

# Repository Goals

The purpose of this project is to demonstrate:

- UiPath workflow design
- Excel automation
- Orchestrator Queue usage
- Configuration management
- Incremental architecture evolution
- Git workflow
- Technical documentation
- REFramework adoption

The project is developed in small, verifiable milestones. Each feature is implemented, tested, documented, and committed before the next enhancement is introduced.
