# Changelog

All notable changes to this project will be documented in this file.

The format is based on Keep a Changelog.

---

## [Unreleased]

### Added

- Repository restructured to support an enterprise Dispatcher–Performer architecture
- New Dispatcher UiPath project
- Git branching strategy (`main`, `develop`, `feature/*`)
- Documentation structure (`docs/`, `config/`)

### Changed

- Renamed `OrderIntakeValidator` to `ValidatorV1`
- Moved Validator V1 under `UiPath/ValidatorV1`
- Output folder now stores only `.gitkeep`; generated Excel files are no longer version controlled

### Planned

- Config.xlsx
- Unique Queue References
- REFramework Performer

---

## [1.0.0] - Initial Release

### Added

- Excel-based Order Intake Validator
- Business-rule validation
- Exception reporting
- Processing summary
- Logging and top-level error handling
