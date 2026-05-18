# TECHNICAL_SPEC.md

## Project Overview
This document establishes the foundational technical specifications for file management, revision control, and documentation standards across all NutriTrack project artifacts. Its purpose is to ensure consistency, maintainability, and efficient collaboration, directly supporting the rapid development and deployment required to achieve user acquisition goals.

## File Naming Conventions
- All filenames must be lowercase, hyphen-separated (kebab-case).
- Use descriptive names that clearly indicate content and purpose.
- Versioning for non-code assets (e.g., design mockups, marketing copy drafts) should follow `filename-vX.Y.ext` (e.g., `onboarding-flow-v1.0.pdf`).
- Code files should not include version numbers in their names, as Git handles versioning.

## Directory Structure
The project workspace will adhere to the following high-level structure. Specific subdirectories will be defined as projects evolve.

- `/`
    - `backend/` (for all server-side code, e.g., API, database models)
    - `frontend/` (for all client-side code, e.g., web app, mobile app)
    - `docs/` (for project documentation, architecture diagrams, process guides)
    - `marketing/` (for marketing assets, campaign plans, content drafts)
    - `data/` (for any static data files, e.g., `campaign_calendar.json`, configuration data)
    - `tests/` (for all unit, integration, and end-to-end tests)
    - `scripts/` (for utility scripts, deployment scripts)
    - `config/` (for environment-specific configurations)
    - `assets/` (for shared design assets, images, icons)

## Revision Control
All code and critical documentation will be managed via Git.

### Branching Strategy
- **main:** Production-ready code. Only merged from `develop` after successful QA and release.
- **develop:** Integration branch for all new features and bug fixes. All feature branches merge into `develop`.
- **feature/[feature-name]:** Short-lived branches for individual features or tasks. Branch off `develop`.
- **bugfix/[bug-name]:** Short-lived branches for bug fixes. Branch off `develop` or `main` for hotfixes.
- **release/[version]:** Created from `develop` for final testing and release preparation. Merges into `main` and `develop`.

### Commit Message Guidelines
- Use imperative mood: "Add feature," not "Added feature."
- First line: concise summary (max 50-72 chars).
- Second line: blank.
- Subsequent lines: detailed explanation of what and why, not how.
- Reference relevant issues or tasks (e.g., `Fix #123`).

## Documentation Standards
- All documentation files will be in Markdown (`.md`) format where possible.
- Code comments should explain complex logic, not obvious code.
- API documentation (e.g., OpenAPI/Swagger) will be generated or maintained alongside the code.

## Asset Management
- Marketing and design assets will be stored in the `assets/` or `marketing/` directories.
- Large binary files (e.g., high-res images, videos) should be managed with Git LFS if necessary.
- All assets must have clear, descriptive filenames.

## Data Management
- Static data files (e.g., `campaign_calendar.json`) will reside in the `data/` directory.
- JSON files should be formatted for readability (indentation).
- Schema for data files should be documented in `docs/` if complex.
