# Changelog

All notable changes to this project will be documented in this file.

The format is inspired by _Keep a Changelog_.

---

## [Unreleased]

### Added

- Dispatcher UiPath project
- Shared `Config.xlsx` for Dispatcher configuration
- Configuration dictionary for runtime configuration lookups
- Standardized Dispatcher logging using configurable `ComponentName` and `Environment`
- Repository documentation
- CHANGELOG.md
- ROADMAP.md
- Architecture documentation
- Design decision documentation
- Mermaid workflow diagrams
- Git branching strategy
- `.gitattributes`

### Changed

- Reorganized repository structure
- Renamed `OrderIntakeValidator` to `ValidatorV1`
- Dispatcher now loads the input file path from `Config.xlsx`
- Dispatcher now loads the Orchestrator queue name from `Config.xlsx`
- Dispatcher now loads configuration into a runtime dictionary
- Dispatcher logging now uses a configurable log prefix
- Removed generated Excel output files from version control
- Added `output/.gitkeep`
- Updated `.gitignore`

---

## [1.0.0]

### Added

- ValidatorV1
- Excel order validation
- Business-rule validation
- Exception reporting
- Processing summary
- Basic logging
- Top-level Try/Catch
- Relative project paths
