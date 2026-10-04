# RPA Order Intake Validator

A UiPath portfolio project that explores order-intake automation using progressively more advanced RPA concepts.

The repository started with a standalone Excel-based validation workflow (**ValidatorV1**) and is being expanded with additional UiPath projects to learn concepts such as Dispatcher–Performer architecture, Orchestrator Queues, configuration management, and REFramework.

The goal is to demonstrate the learning journey by keeping each stage functional, documented, and version controlled.

---

## Repository layout

The repository currently contains multiple UiPath projects.

| Project         | Purpose                                                |
| --------------- | ------------------------------------------------------ |
| **ValidatorV1** | Standalone Excel validation workflow                   |
| **Dispatcher**  | Reads orders from Excel and creates queue transactions |
| **Performer**   | Planned transaction processor using REFramework        |

---

## ValidatorV1

ValidatorV1 reads an Excel file containing customer orders, validates each order against business rules, and produces:

- `validated_orders.xlsx`
- `exceptions.xlsx`
- `processing_summary.xlsx`

It demonstrates:

- UiPath Studio workflow development
- Excel automation
- DataTable processing
- Business-rule validation
- Business exception handling
- Multiple exception reasons for a single row
- Basic logging
- Top-level Try/Catch error handling
- Relative project paths

---

## Repository structure

```text
uipath-order-intake-validator/
│
├── README.md
├── CHANGELOG.md
├── ROADMAP.md
├── .gitignore
├── .gitattributes
│
├── docs/
│   ├── architecture.md
│   ├── decisions.md
│   └── diagrams.md
│
├── config/
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

## Running ValidatorV1

1. Clone the repository.

2. Open:

```text
UiPath/ValidatorV1/project.uiproj
```

3. Run `Main.xaml`.

Generated output files are written to the `output` folder.

The generated Excel files are intentionally excluded from Git and are recreated each time the workflow runs.

---

## Documentation

Additional documentation is available in the `docs` folder.

| Document          | Description                              |
| ----------------- | ---------------------------------------- |
| `architecture.md` | Overall project architecture             |
| `decisions.md`    | Design decisions made during development |
| `diagrams.md`     | Mermaid workflow diagrams                |

---

## Roadmap

The planned evolution of the project is documented in **ROADMAP.md**.

---

## Changelog

Project history is maintained in **CHANGELOG.md**.

---

## License

This repository is provided for learning and portfolio purposes.
