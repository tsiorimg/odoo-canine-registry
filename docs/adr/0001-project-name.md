# ADR 0001: Project name

- Status: Accepted
- Date: 2026-08-14

## Context

The initial product idea is inspired by the needs of a national canine registry in Madagascar. The project does not yet have authorization to represent or reuse the identity of a specific organization.

## Decision

The public working name is **Open Canine Registry** and the repository name is `odoo-canine-registry`.

Python packages and Odoo addons should use neutral `canine_` names. Organization-specific names and branding must remain outside the generic core unless permission and a clear integration boundary exist.

## Consequences

- The project can be developed publicly without implying official endorsement.
- The core can be reused for other registries.
- A future organization-specific deployment may add a separate configuration or localization addon.
