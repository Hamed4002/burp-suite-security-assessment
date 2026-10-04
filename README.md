# Web Application Security Assessment — OWASP Mutillidae II

A security assessment of **OWASP Mutillidae II**, a deliberately
vulnerable web application, performed with **Burp Suite** in the role of
a security analyst: mapping the attack surface, building a threat model,
exploiting five vulnerability categories with documented
proof-of-concept, and translating each finding into a concrete secure
coding fix.

> Final project for *Secure Programming*, Shahed University.

## Scope

- **Target:** [OWASP Mutillidae II](https://github.com/webpwnized/mutillidae), run locally on XAMPP (security level 0)
- **Tooling:** Burp Suite Community Edition, Firefox (proxied through Burp)
- **In scope:** authentication, access control, input validation, session management, the application's own endpoints
- **Out of scope:** anything outside the local test environment, automated scanning, DoS, destructive abuse beyond a proof-of-concept

## Report structure

| Section | Contents |
|---|---|
| [`docs/01-target-overview.md`](docs/01-target-overview.md) | App introduction, user roles, entry points, attack surface |
| [`docs/02-threat-model.md`](docs/02-threat-model.md) | Assets, likely attackers, attack scenarios, threat model diagram |
| [`docs/03-methodology.md`](docs/03-methodology.md) | Tools, test environment setup, Burp Suite workflow |
| **Findings** | |
| [`docs/findings/01-sql-injection.md`](docs/findings/01-sql-injection.md) | Critical — authentication bypass via SQLi |
| [`docs/findings/02-broken-authentication.md`](docs/findings/02-broken-authentication.md) | High — no rate limiting, user enumeration |
| [`docs/findings/03-csrf.md`](docs/findings/03-csrf.md) | High — CSRF token present but never validated |
| [`docs/findings/04-xss.md`](docs/findings/04-xss.md) | High — stored & reflected XSS |
| [`docs/findings/05-broken-access-control.md`](docs/findings/05-broken-access-control.md) | Medium — admin pages reachable by any user |
| [`docs/04-risk-summary.md`](docs/04-risk-summary.md) | Consolidated risk table and prioritization |
| [`docs/05-conclusion.md`](docs/05-conclusion.md) | Lessons learned and recommendations |

## Risk summary

| Vulnerability | Risk | Impact | Likelihood |
|---|---|---|---|
| SQL Injection | **Critical** | High | High |
| Broken Authentication | High | High | High |
| CSRF | High | High | High |
| XSS (Stored & Reflected) | High | High | High / Medium |
| Broken Access Control | Medium | Medium–High | High |

**4 of 5 findings (80%) rate High or Critical.** SQL Injection, XSS,
Broken Authentication, and Broken Access Control each map directly to
their own OWASP Top 10 (2021) category; CSRF is no longer a standalone
category in the 2021 list but remains a well-documented, widely exploited
flaw (CWE-352), conceptually covered under Broken Access Control. Full
detail, root-cause analysis, and remediation per finding are in
[`docs/findings/`](docs/findings).

## Disclaimer

All testing was performed against a local, deliberately vulnerable
instance of Mutillidae running on our my machine, strictly for
coursework. None of this targets, or should be used against, software
you don't own or have explicit permission to test.
