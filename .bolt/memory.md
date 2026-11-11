# Project memory

## Product intent & audience

- Smart Campus Room Availability Checker — Software Engineering Practice Work #10.
- User inputs a start/end/now time to check whether a single fictional room (R1) can be booked.
- Audience: grading/instructors for the practice assignment; must satisfy AC1–AC6.

## Brand personality & voice

- Academic, factual, minimal; UI copy mirrors AC acceptance-criteria language.
- Feedback messages are plain-text and per-field, separate from availability result.

## Visual design & UX direction

- React + Vite + TypeScript starter (`vite-react-typescript-starter`, version 0.0.0).
- Three time inputs (start, end, now) + Check Availability button + result panel; no room selector, capacity/equipment filters, or attendees field (to be removed in pending patch).
- Desktop and mobile must both show clear validation + result feedback.
- Icons via `lucide-react`; only `SearchX` import will be dropped post-patch.

## Decisions, constraints & rationale

- Acceptance criteria AC1–AC6 are authoritative behavior constraints: time validation, 120-minute max booking length, blocked-room rejection, overlap detection, endpoint contact (canBook), no mutation of booking data, clear feedback on desktop & mobile.
- R1 booking fixture: `{ start: 600, end: 660 }`; DEFAULT_NOW = 540 (09:00).
- Time represented in minutes (integer); `parseWholeNumber` parses raw strings.
- `canBook(start, end, now, blocked, bookings)` is the core availability endpoint; tests call it directly for AC3 blocked-room coverage independent of catalog.
- Blocked-room rejection must remain covered by a test fixture (`tests/regression_ac.test.ts`).
- Pending minimal patch (awaiting approval): remove RoomFilters, filtering.ts, filtering.test.ts; simplify App, searchController, validation; update controller_integration, ui_smoke, demo_scenarios. No edits made yet.
- All verification commands pass: npm test (34/34), typecheck, lint, build.

## Open questions & assumptions

- Approval to apply the R1-only patch has not yet been given; files remain unchanged.
- Assumed that `capacity`/`equipment` fields stay on the `Room` type as factual attributes even though filter UI is removed.
- Assumed existing `regression_ac.test.ts` inline blocked-room fixtures are sufficient coverage after multi-room removal.