# Agent Instructions

## Repository Overview

This repository serves as a template for Layer5 projects.

These instructions provide general guidance for AI coding agents
working with repositories created from this template.

## Source of Truth

AGENTS.md is the canonical source of instructions for AI coding agents.

CLAUDE.md is a symbolic link pointing to AGENTS.md.

Contributors should only edit AGENTS.md to update agent instructions.

Do not maintain a separate copy of these instructions in CLAUDE.md.

## Project Structure

- README.md: Project overview and documentation.
- CONTRIBUTING.md: Contribution guidelines.
- Makefile: Available development and build commands.
- .github/workflows/: GitHub Actions workflows and CI configuration.
- .github/: Issue templates and repository configuration.

## Development Guidelines

1. Read README.md before making changes.
2. Follow the guidelines in CONTRIBUTING.md.
3. Inspect the Makefile to identify available build and test commands.
4. Follow the existing coding conventions.
5. Keep changes focused and well documented.
6. Run the relevant available tests before submitting a pull request.

## Agent Skills

When available, consult area-specific agent skills located at:

.agents/skills/<area>/SKILL.md

Follow the instructions applicable to the area being modified.

## Generated Files

Do not manually edit generated files.

Instead, locate the original source and use the project's documented
generation process.

Repository-specific generated files and generation commands should
be documented when this template is adapted for a project.

## Repository-Specific Instructions

Repositories created from this template should document:

- Project purpose and architecture.
- Required development tools and versions.
- Setup and build commands.
- Testing and linting commands.
- Generated files that must not be edited manually.
- Additional project-specific coding conventions.

## Contributions

Follow CONTRIBUTING.md when submitting changes.

Review the relevant tests and documentation before opening a pull request.