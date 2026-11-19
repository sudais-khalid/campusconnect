# Security Policy

CampusConnect handles complaints about university staff and services, sometimes filed anonymously. We take the confidentiality of that data seriously and welcome responsible reports.

## Supported versions

| Version | Supported |
|---|---|
| `main` (deployed continuously) | Yes |
| Older commits | No |

## Reporting a vulnerability

**Please do not open a public issue for security problems.**

Report privately through GitHub: open the repository's **Security** tab and choose **Report a vulnerability**. Include:

- what is affected (page, API route or file) and the impact you expect;
- steps to reproduce, with the role you were signed in as;
- any proof of concept, kept to the minimum needed to show the issue.

What to expect:

| Step | Target time |
|---|---|
| Acknowledgement | 3 working days |
| First assessment and severity | 7 working days |
| Fix for critical or high issues | 14 days |

We credit reporters in the release notes unless you prefer to stay anonymous.

## Scope

In scope: the application code in this repository and the live demo at <https://campusconnect-delta-topaz.vercel.app>.

Out of scope: denial-of-service and load testing, social engineering, physical attacks, issues in third-party services (Vercel, Neon, Upstash) that are not caused by our configuration, and reports from automated scanners without a demonstrated impact.

Please test only with the published demo accounts, do not access or modify other people's data, and stop as soon as you have shown the issue.

## How the application is protected

| Area | Control |
|---|---|
| Access control | Role and ownership rules are applied inside every database query, not only in the interface. Out-of-scope access returns 403 and is written to an audit log. ([details](docs/05-security-and-access-control.md)) |
| Authentication | Email verification, scrypt password hashing, revocable database sessions, two-step verification for staff, 12-hour cap on staff sessions. |
| Abuse | Rate limits on sign-in, registration, complaints, uploads, comments and exports. |
| Input | Every request is validated with Zod; unknown fields are dropped, so clients cannot set department, status or ownership. Output is escaped by React; raw HTML rendering is blocked by lint rules. |
| Files | Images are checked by content, re-encoded to WebP (removing EXIF and GPS data), stored privately and served only after the complaint access check. |
| Privacy | Anonymous complaints hide the student from departments; identity reveals require a reason and are audited. Push and email messages contain no complaint details. Logout clears the device's saved data. |
| Transport and headers | HTTPS only with HSTS, `nosniff`, frame denial, strict referrer policy and a restrictive API content security policy. |
| Supply chain | Locked dependencies, Dependabot updates, CI that type-checks, lints, tests and builds every change. |
| Secrets | Kept in the hosting provider's encrypted environment settings, never in the repository. |
