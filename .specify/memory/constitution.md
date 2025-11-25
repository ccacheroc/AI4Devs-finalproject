# Constitution — NeighbourhoodAssociationAPI

Version: 1.0.0
Ratified: 2025-11-25
Last modified: 2025-11-25

Purpose

This document is the canonical constitution for the SpecKit project "NeighbourhoodAssociationAPI". It is the authoritative reference for human contributors and AI assistants working on the repository. The constitution defines the required technology stack, architectural principles (Clean Architecture + DDD), testing discipline (TDD + BDD), API rules, data protection considerations (GDPR), repository layout, and mandatory rules for AI agents.

1. Tech stack and general rules

- Backend language: Python 3.11+.
- Web framework: FastAPI (async). Use type hints everywhere and keep HTTP layer strictly separated from domain/application layers.
- Persistence: Relational database (PostgreSQL). Use a repository pattern; controllers/routers MUST NOT perform direct ORM queries.
- Testing: pytest for unit, integration and API tests. Use a BDD tool (pytest-bdd or behave) for high-level behavioural tests.
- Frontend: Minimal client only for exploring and testing the API: a tiny React + Vite app (preferred by spec) with no complex state management; only "call endpoint, show response" behaviour.
- Tooling: use `uv` for managing Python dependencies (as specified), `ruff` for linting/formatting, and `mypy` for static typing checks.
- Formatting: follow ruff and project black configuration.
- Rule: Any AI-generated code must respect this stack and must NOT change it silently. New libraries or major changes require an ADR and an explicit PR reviewed by humans.

2. Architecture principles (Clean Architecture + DDD)

Layers (inner -> outer):
  - Domain layer: Entities, Value Objects (VOs), Aggregates, Domain Events, Domain Services. Pure Python, framework-agnostic, no I/O.
  - Application (Use-case) layer: Application services / use cases that orchestrate domain logic. Define ports (interfaces) for repositories and external services.
  - Infrastructure layer: ORM mappers, database adapters, email, external APIs, logging, migrations (Alembic). Implements the ports.
  - Interface / Delivery layer: FastAPI routers, Pydantic DTOs, authentication guards and the minimal frontend used for testing.

Rules:
- Inner layers MUST NOT depend on outer layers. Domain and Application must never import FastAPI, SQLAlchemy, HTTP types, or other infra classes.
- Repository interfaces (ports) live in domain/application; implementations live in infrastructure.
- Map DTOs -> Domain objects at the edge (interfaces) as early as possible.

DDD guidelines:
- Identify bounded contexts when the domain grows, e.g. "Membership & Fees", "Incidents & Maintenance", "Meetings & Agreements".
- Model aggregates to protect invariants (e.g., Meeting aggregate with AgendaItem and Agreement children).
- Keep a ubiquitous language: neighbour, dwelling, fee, payment, incident, meeting, minute, agreement, announcement.

3. Testing strategy (TDD)

TDD cycle:
- Red → Green → Refactor. No production code without a failing test first.

Types of tests:
- Unit tests: target domain entities, VOs and use cases. No DB, no HTTP, no external services.
- Integration tests: exercise repository implementations and DB integration (use test Postgres, containers or ephemeral DBs).
- API / E2E tests: use FastAPI test client (httpx) to verify request/response behaviour and main happy/error flows.

Quality bar:
- Coverage requirement: 95% for domain + application layers.
- Tests must be deterministic and isolated. Avoid non-deterministic or flaky tests.
- Mock only external boundaries (DB drivers, HTTP clients). Do NOT mock domain behaviour.
- Use hypothesis property-based tests where meaningful (e.g., VO validation), but keep strategies simple and seeded to avoid flakiness.

AI rule: Any behavioral or API change proposed by an AI must include failing tests (unit + BDD) and must not remove existing tests unless a documented and justified refactor accompanies the change.

4. Behaviour-Driven Development (BDD) practices

- User stories: write using a consistent template: "As a <role> I want <capability> so that <benefit>". Include acceptance criteria.
- Scenarios: write Gherkin scenarios (Feature, Scenario, Given/When/Then) for key behaviours such as:
  - Paying membership fees
  - Creating and resolving incidents
  - Scheduling and closing meetings
  - Notifying neighbours about announcements or decisions
- Living documentation: BDD scenarios are executable documentation. Place features in `ai-specs/` and step definitions under `tests/bdd/`.

AI workflow for new features:
1. Propose or update the user story(s).
2. Add/update Gherkin scenarios.
3. Implement tests (TDD) and then code.

5. API design rules

- Style: RESTful resource design, proper use of HTTP verbs and status codes. Expose OpenAPI via FastAPI.
- Versioning: mount API under `/api/v1/`. Breaking changes require bumping the version and an ADR.
- DTOs: use Pydantic models for input and output DTOs in the interfaces layer. Validate at the edge and map to domain VOs immediately.
- Error handling: unified error format: `{ "error": { "code": "string", "message": "string", "details": {...} } }`. Do not leak stack traces or internal exceptions.
- Security: use JWT (Bearer) or equivalent. Enforce least privilege for roles: admin, member, guest. Authorization rules belong to application layer (not only controllers).
- Internationalization: domain context follows Spanish terminology but API paths and models should remain consistently English.

6. Data protection and ethics

- The system will handle personal data (names, emails, addresses). Assume applicability of EU GDPR and Spanish law.
- Principles: data minimization, purpose limitation, and retention minimization.
- Provide mechanisms for data access, rectification and deletion where legally allowed. Expose endpoints and internal procedures for subject requests.
- Log access to sensitive operations (e.g., changes to owner data, full exports). Do not log PII in clear text—mask or redact sensitive fields.
- Secrets: do NOT store secrets in the repository. Use environment variables and pydantic-settings for configuration.
- Tests must NOT rely on real user data. Anonymize test fixtures and snapshots.

7. Repository structure and naming conventions

Recommended layout (strict unless ADR states otherwise):

```
src/neighbourhood_association/
  domain/
  application/
  infrastructure/
  interfaces/
tests/
  unit/
  integration/
  api/
  bdd/
frontend/  # minimal React + Vite app
ai-specs/  # Gherkin features and related specs
.specify/
docs/adr/
alembic/
pyproject.toml (or requirements.txt / uv lock)
Dockerfile
docker-compose.yml
constitution.md
```

Naming conventions:
- Use typing.NewType for domain IDs (e.g. MemberID = NewType("MemberID", str)).
- Value Objects: dataclasses with `frozen=True`.
- Entities: dataclasses with explicit identity and factory methods when needed.
- Modules: snake_case. Classes: PascalCase.

8. Rules for AI assistants and SpecKit

The AI MUST:
- Respect architecture boundaries (no domain code inside HTTP handlers).
- Make small, incremental changes with clear diffs and explanations.
- Always provide/modify tests (unit + BDD) that demonstrate behaviour changes.
- Update or propose ADRs when introducing new frameworks or changing the stack.

The AI MUST NOT:
- Change public API signatures without an explicit specification and version bump.
- Bypass TDD/BDD or add large untested code blobs.
- Mix concerns (e.g., put DB or HTTP code in domain objects).

9. Per-feature checklist (mandatory before merge)

- [ ] Add/update user story and Gherkin scenarios in `ai-specs/` and `tests/bdd/` (if applicable).
- [ ] Add a failing unit test that exercises the behaviour (Red).
- [ ] Implement minimal production code to make tests pass (Green).
- [ ] Add integration / API tests if the change touches infrastructure or interfaces.
- [ ] Provide an in-memory fake adapter in `infrastructure/` for tests and a concrete adapter for production.
- [ ] Run linters and `mypy` and fix issues.
- [ ] Add/update documentation and docstrings (example usage in docstring).
- [ ] Ensure error mapping from infra to app/domain and standardized error response.
- [ ] Run BDD scenarios and ensure they pass.
- [ ] Review GDPR/data retention impact and add notes if applicable.

10. ADRs, governance and change process

- Any significant decision (new dependency, stack changes, API contract changes) requires an ADR in `docs/adr/` using the standard ADR template (title, date, state, context, decision, consequences, authors).
- Changes to this constitution require a PR labeled `contrib/constitution` and explicit approval by the project owner.
- Version the constitution using semantic versioning. Major changes require sign-off from maintainers.

11. CI and quality gates (recommended)

- CI must run: ruff, mypy, pytest (unit + integration), and BDD test suite. Enforce coverage threshold for domain + application layers (95%).
- PRs touching sensitive areas (auth, data export, deletion) must include a "Privacy & Security review" section in the PR description.

12. Emergency and rollback process

- If a change causes a production incident:
  1. Open an incident ticket.
  2. Roll back to the last stable release.
  3. Run regression tests in staging.
  4. Produce a postmortem and file an ADR if the incident reveals design weaknesses.

13. Examples and minimal contracts

- DTO mapping example (summary):
  - `interfaces/dtos.py`: Pydantic models for request/response.
  - `interfaces/controllers.py`: validate DTO, map to domain VO/entity, call application use case.
  - `application/use_cases/*.py`: typed inputs and typed results or domain events.
  - `infrastructure/repositories/postgres.py`: concrete repository implementing repository port.

14. Style and coding rules

- Use `ruff` for linting and formatters per project config.
- Use `mypy` for static typing checks; document any relaxations in `pyproject.toml`.
- All public functions and classes require concise docstrings with a minimal usage example.

15. Prohibitions (strict)

- Never mix I/O, DB or HTTP code into domain/application layers.
- Never commit secrets into the repository.
- Never return stack traces or internal errors to API clients.

Document lifecycle

This constitution is a living document. Any amendment must follow the governance process described above and be recorded with versioned ADRs. AI agents must follow it as the canonical policy for code generation and changes.

Quick summary

Project: NeighbourhoodAssociationAPI
Constitution version: 1.0.0 (2025-11-25)
Mandates: FastAPI, PostgreSQL, Clean Architecture + DDD, strict TDD/BDD, GDPR compliance, and explicit AI rules.

