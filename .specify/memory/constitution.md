<!--
Sync Impact Report
Version change: unratified template → 1.0.0
Modified principles:
- Template Principle 1 → I. Clean Code
- Template Principle 2 → II. Simple UX
- Template Principle 3 → III. Responsive Design
Added sections: Additional Constraints; Development Workflow
Removed sections: None
Follow-up TODOs: Record the original ratification date when known.
-->

# Login App Demo Constitution

## Core Principles

### I. Clean Code
Code MUST be readable, cohesive, and maintainable. Names MUST communicate intent;
each module MUST have a clear responsibility; duplication and unnecessary
complexity MUST be avoided. Changes MUST follow the repository's established
patterns and pass the applicable lint, type-check, and test checks. These rules
keep the application easy to change without introducing avoidable regressions.

### II. Simple UX
User-facing flows MUST make their purpose and next action clear. Common tasks
MUST use consistent, familiar controls and avoid unnecessary steps. The
interface MUST provide understandable feedback for user actions, including
validation errors and completed or failed operations. Simplicity reduces user
effort and makes behavior predictable.

### III. Responsive Design
Every user-facing page and interaction MUST remain usable across narrow mobile,
tablet, and desktop viewports. Layouts MUST adapt to available space without
unintended horizontal scrolling, clipped content, or controls that become
unusable. Responsive behavior MUST be checked at representative viewport sizes
when a UI change is made.

## Additional Constraints

The application MUST retain the framework, dependencies, and conventions
already established by the repository unless a change is justified by the
feature requirements. New dependencies and architectural complexity MUST be
limited to what is necessary to meet those requirements.

## Development Workflow

Changes MUST be reviewed against these principles before completion. UI changes
MUST be checked at representative mobile and desktop viewport sizes. Relevant
automated checks MUST be run for changed behavior, and any check that cannot
be run MUST be identified in the change summary.

## Governance

This constitution governs project design and implementation decisions.
Amendments MUST update this document, explain their impact, and receive review
alongside the work they govern. The version follows semantic versioning:
MAJOR for incompatible governance changes, MINOR for new or materially
expanded principles or sections, and PATCH for clarifications and wording
changes. Reviews MUST verify that changes comply with the principles and that
relevant quality checks have been completed or explicitly reported.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): original adoption date not recorded | **Last Amended**: 2026-10-09
