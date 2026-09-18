<!--
Sync Impact Report
- Version change: UNRATIFIED -> 1.0.0
- Modified principles: template placeholders -> I. Server-Side Business Rules; II. Explicit UI
  Loading and Error States; III. Automated Coverage for Pricing and Limits; IV. Database-Authoritative
  Ticket Availability
- Added sections: Product and Technical Constraints; Development Workflow and Quality Gates
- Removed sections: fifth principle slot from the resolved template, because the user specified
  four principles
- Follow-up TODOs: Confirm the original ratification date.
-->

# Spec Kit Project Constitution

## Core Principles

### I. Server-Side Business Rules
All business rules MUST be validated and enforced on the server. Client-side validation
MAY improve usability, but it MUST NOT be the only enforcement point and MUST NOT be
treated as authoritative. The server MUST reject invalid, unauthorized, or inconsistent
requests regardless of the client implementation. This prevents bypasses and keeps all
clients subject to the same domain rules.

### II. Explicit UI Loading and Error States
Every production screen MUST define and render an explicit loading state and an explicit
error state for each asynchronous data dependency. A screen MUST NOT silently appear
empty, remain indefinitely in a pending state, or present stale data as successful content
when loading or retrieval fails. These states are required for predictable user feedback
and diagnosable production behavior.

### III. Automated Coverage for Pricing and Limits
Every pricing rule and every limit rule MUST be covered by automated tests. Coverage MUST
include normal behavior and relevant boundary conditions, including the applicable lower,
upper, zero, and invalid cases. A change to pricing or limits MUST update or add tests
that demonstrate the intended behavior before the change is considered complete. This
protects revenue, entitlement, and capacity decisions from regressions.

### IV. Database-Authoritative Ticket Availability
The database MUST be the source of truth for ticket availability. The screen state, cached
client state, or previously fetched availability MUST NOT be used as the final authority
when reserving, selling, or otherwise changing ticket inventory. Availability-changing
operations MUST re-check authoritative state in the database and MUST handle concurrent
requests according to the database transaction and consistency guarantees. This prevents
overselling caused by stale UI state.

## Product and Technical Constraints

The system MUST preserve the four core principles across web clients, server endpoints,
background jobs, integrations, and administrative tools. Client-side safeguards are
usability features, not security or domain guarantees. Any implementation that cannot
meet these constraints MUST document the exception, its risk, and its compensating
controls before approval.

## Development Workflow and Quality Gates

Code review MUST verify server-side enforcement for business rules, loading and error
states for production screens, automated tests for pricing and limits, and database
authority for ticket availability. Changes affecting ticket inventory MUST include
concurrency-aware tests or an equivalent verification of the relevant transaction
behavior. Work is not complete until these quality gates are satisfied or an explicitly
approved exception is recorded.

## Governance

This constitution supersedes conflicting development practices for this project.
Amendments MUST describe the affected principles, rationale, migration impact, and
required follow-up work. The amendment MUST be reviewed by the project maintainers
before it is adopted, and affected plans, tasks, and implementations MUST be aligned
with the amended rules.

The constitution uses semantic versioning. MAJOR increments indicate incompatible
principle removals or redefinitions; MINOR increments indicate added principles or
materially expanded governance; PATCH increments indicate clarifications, wording
changes, or other non-semantic refinements. Every pull request MUST include a compliance
review against this constitution when its scope touches a governed area.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): confirm original adoption date | **Last Amended**: 2026-09-17
