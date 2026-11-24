---
name: docs-guidance
description: Documentation standards and markdown guidelines for Layer5 projects. Use when writing or updating READMEs, guides, API documentation, or architecture docs.
---

# Documentation Guidance Skill

Standards for writing and maintaining documentation in Layer5 projects.

## Documentation Rules

1. **Format & Style**:
   - Standard GitHub-flavored Markdown.
   - Relative links for repository files; absolute URLs for external references.
   - Clean headings without redundant blank lines.

2. **Generated Documentation**:
   - Never manually edit docs generated from code annotations or schemas.
   - Run the documented generator command (e.g., `make gen-docs`) when modifying source docstrings.

3. **Link Integrity**:
   - Test all added links for 404s.
   - Ensure anchors match heading text.
