# ADR 0002: Project license

- Status: Accepted
- Date: 2026-08-14

## Context

The project is an Odoo 19 Community web application intended for public collaboration and possible operation as a network service. The project should remain open when modified and deployed for users over a network.

## Decision

Project-authored source code is licensed under **GNU Affero General Public License v3.0 or later (AGPL-3.0-or-later)** unless a file explicitly states otherwise.

Third-party dependencies and assets retain their respective licenses and must be documented.

## Consequences

- Source code and distributed modifications must remain available under the license terms.
- Network deployment of modified versions carries source-availability obligations.
- Contributors must verify the compatibility of added dependencies, code, and assets.
- Unauthorized proprietary code, data, or media must not be committed.
