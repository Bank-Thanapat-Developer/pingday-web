# PingDay Web Decision Log

## ADR-001: Use Next.js App Router with strict TypeScript

### Decision

The frontend will use Next.js App Router and strict TypeScript, subject to compatibility checks when the intended repository is restored.

### Reason

This provides a maintained React application structure with typed boundaries and clear route composition.

### Alternatives considered

Pages Router or a non-Next.js React application.

## ADR-002: Centralize API communication

### Decision

Feature code will use a shared API client/service boundary instead of issuing ad hoc requests throughout components.

### Reason

One boundary can handle base URL configuration, response typing, and consistent API errors.

### Alternatives considered

Calling `fetch` independently from each component.
