# ADR 0003: Odoo module topology

- Status: Accepted
- Date: 2026-08-14

## Context

Open Canine Registry will grow into multiple Odoo addons covering registry, breeding, validation, portal, website, documents, and payment workflows.

The project needs a stable dependency topology that:

- isolates extensions of Odoo base models;
- prevents circular dependencies between functional addons;
- provides one explicit application entry point for installation;
- keeps business logic out of the installation aggregator;
- remains verifiable automatically in continuous integration.

## Decision

The project uses two mandatory foundation addons: `canine_base` and `canine_app`.

### `canine_base`

- Depends exactly on the Odoo `base` addon.
- Is declared with `application: False` and `auto_install: False`.
- Contains only extensions of base models and shared primitives compatible with the `base`-only dependency constraint.
- Must not contain registry, breeding, portal, website, accounting, payment, messaging, or other feature logic that requires additional Odoo addons.

Every functional project addon must depend directly or indirectly on `canine_base`.

### `canine_app`

- Is declared with `application: True` and `auto_install: False`.
- Is the single explicit installation entry point for the complete project.
- Depends on `canine_base` and, progressively, on every functional addon required by the application.
- Contains no models, business logic, security rules, functional views, or workflows.
- Must never be listed as a dependency of another project addon.

Local development, CI installation tests, demonstration environments, and deployments install or upgrade `canine_app`.

## Consequences

### Positive

- Base-model extensions have a predictable and minimal dependency surface.
- Installing `canine_app` installs the complete current application.
- Functional addons can be developed and tested independently.
- The dependency graph has a clear foundation and a clear installation entry point.
- CI can detect invalid dependencies and cycles before merge.

### Constraints

- Code requiring `mail`, `portal`, `website`, `account`, `payment`, or another addon cannot be placed in `canine_base`.
- The `canine_app` manifest must be updated whenever a functional addon becomes part of the standard installation.
- No business implementation may be placed in `canine_app`.
- Dependency-topology validation is a required CI responsibility.
