# PingDay Web Project Plan

## Overview

PingDay is a personal reminder system for one-time and yearly events, with notifications sent through the backend and LINE. This repository will contain the responsive Next.js client; the Go API lives in `pingday-api`.

## Current Phase and Constraints

Phase 0 inspection found this directory empty: no source files, `package.json`, Next.js app, README, tests, or `.git` metadata are present. Repository history and Git status cannot be inspected, and there is no existing test/build baseline. Confirm the intended repository checkout before implementation.

## Architecture

Use Next.js App Router and strict TypeScript. Keep route composition in `src/app`, reusable UI in `src/components`, feature-specific behavior under `src/features`, shared API access in `src/services` or `src/lib/api`, and shared contracts/utilities in focused modules. UI components should not scatter raw fetch calls; the API client should centralize base URL, JSON handling, and error mapping.

Proposed structure (adapt to the confirmed Next.js version and existing conventions):

```text
src/app/
src/components/
src/features/events/
src/features/dashboard/
src/features/notifications/
src/hooks/
src/lib/api/
src/services/
src/types/
src/constants/
src/utils/
public/
tests/
docs/
.env.example
.gitignore
Dockerfile
package.json
README.md
```

## Technology Decisions

- Next.js App Router, React, and strict TypeScript.
- Use the package manager and lint/format conventions already present once the intended checkout is available; otherwise choose and document them at initialization.
- Centralize API communication in a reusable client. Keep API base URL in environment configuration and never put secrets in browser-exposed variables.
- Prefer accessible, responsive, component-based UI with explicit loading, empty, and error states.
- Select a test runner compatible with the installed Next.js version during Phase 1.

## Development Phases and Milestones

0. Workspace analysis and planning (current): inspect both repositories and record their state; no application feature work.
1. Foundation: Next.js/TypeScript foundation, lint/format, environment configuration, base layout, reusable API client, and first tests.
2. Event domain UI: list, create, edit, view, activate/deactivate, delete confirmation, and form behavior tests.
3. Reminder rule UI: recurrence and reminder interval selection.
4. Coordinate API contract and scheduler behavior with backend.
5. LINE integration is backend-owned; provide only UI/API support needed by agreed contract.
6. Dashboard: upcoming events, days remaining, reminders, and recent notification status.
7. Quality: accessibility/responsive review, tests, API docs/types alignment, Docker and docs improvements.
8. CI/CD preparation only when requested; deployment remains postponed.

## Phase 1 Implementation Checklist

- [ ] Confirm/restore the intended Git checkout; inspect current files and status before initialization.
- [ ] Record Node.js and package manager versions; select compatible stable Next.js and React versions.
- [ ] Initialize App Router and strict TypeScript only if not already present.
- [ ] Configure ESLint and Prettier consistently with installed versions.
- [ ] Add environment variable validation and `.env.example`; keep secrets server-side.
- [ ] Add minimal responsive base layout and global styles.
- [ ] Add reusable API client with typed request/response handling and normalized errors.
- [ ] Set up a compatible unit/component test runner and one meaningful foundation test.
- [ ] Add a multi-stage Dockerfile and production build configuration if appropriate for the chosen Next.js output mode.
- [ ] Document setup, environment, tests, lint, typecheck, and build commands in README.
- [ ] Run lint, formatting check, typecheck, tests, and build; report actual results.

## API Contract Plan

The client will target the backend's `/api/v1` endpoints. Planned initial needs include event CRUD, upcoming events, and notification history, subject to MVP review. Avoid duplicating backend contracts manually where OpenAPI generation becomes practical. Centralize mapping of API errors to user-facing states.

## Testing Strategy

Use behavior-based tests for API client error handling, forms, recurrence/reminder selection, and loading/empty/error states. Avoid snapshots as a substitute for behavior. Keep tests independent of a live backend where practical by mocking the API client boundary.

## CI/CD Plan

Prepare consistent lint, typecheck, test, and production build scripts for a future CI pipeline. Cloud deployment is explicitly out of scope.

## Deployment Plan

No cloud deployment in this phase. Container support may be prepared after the app's production output mode is established.

## Future Improvements

OpenAPI-generated API types, custom reminder intervals, richer notification history filters, and UI polish based on real usage.
