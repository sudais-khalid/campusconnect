# Contributing to CampusConnect

Thank you for helping improve CampusConnect. This guide keeps changes consistent and safe.

## Getting started

1. Fork and clone the repository, then follow [Run locally](README.md#run-locally).
2. Create a branch from `main`: `feat/short-name`, `fix/short-name` or `docs/short-name`.
3. Read the [backend guide](docs/12-backend-guide.md) and the [frontend design system](docs/13-frontend-design.md) before larger changes.

## Rules that keep the system safe

- Load complaints only through the scoped repository (`src/modules/complaints/repository.ts`). Never query complaints directly from a page or route.
- Validate every input with Zod at the boundary.
- Route handlers stay thin: validate, call a service, respond. They must not import the database client (lint enforces this).
- Schema changes need a Prisma migration, written so the previous release still works (add first, remove later).
- No secrets, real student data or production database dumps in commits, issues or screenshots.

## Before opening a pull request

```bash
npm run typecheck
npm run lint
npm test
npm run build
```

For access-control or workflow changes, also run `node scripts/smoke-test.mjs` against a local server with seeded data.

## Commits and pull requests

- Use [Conventional Commits](https://www.conventionalcommits.org/): `feat(complaints): add reopen limit`.
- Keep pull requests focused; fill in the template, link the requirement (FR or FX number) and add screenshots for UI changes (phone and desktop).
- Update the docs in `docs/` when behaviour, the API or the data model changes, then run `npm run docs:build`.

## Reporting bugs and ideas

Use the issue templates. Security problems go through private reporting instead; see [SECURITY.md](SECURITY.md).

By contributing you agree that your work is released under the [MIT License](LICENSE) and that you will follow the [Code of Conduct](CODE_OF_CONDUCT.md).
