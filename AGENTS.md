# Agent instructions

Write all code comments and documentation in English.

## Product boundary

- cpmt is a reusable entitlement-only payment helper for cvld admission.
  An independent intermediary owns the billing relationship and customer
  records. cpmt proves a member-bound entitlement is currently valid with
  expiry, without customer/payment ids the operator could resolve.
- A webhook filter we operate or a restricted API key we could expand does
  not meet the boundary. Standard merchant-of-record dashboards/exports
  that expose customer records fail closed here: host must verify the
  intermediary enforces entitlement-only access via portal, API, export
  and support before wiring it.
- GNU Taler, wallet funding and coins are rejected per contract. Automatic
  recurring charges with provider-managed renewals, failures, cancellation
  and billing support are required. cvld receives current eligibility only.
- This crate is LGPL-3.0-only WITH LGPL-3.0-linking-exception: combined works
  may link statically or dynamically without relinking duties; library
  modifications stay LGPL. Do not add implementation code available
  only under the full GPL or AGPL.
- No live billing in tests. Fixtures only. No spending, registration or outreach.

## Quality boundary

- `cargo fmt --check`, `cargo clippy --all-targets` (no warnings),
  `cargo test` — all green before every commit. No local workstation
  builds per task status; use GHA, Crow fallback while GHA is down.
- Validate member binding, expiry, replay protection and uniform errors
  with fixtures. Settlement reports must not recreate per-member mappings.
