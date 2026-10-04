# Risk Summary

## Consolidated risk table

| Vulnerability | Risk Level | Impact | Likelihood |
|---|---|---|---|
| SQL Injection | Critical | High | High |
| Broken Authentication | High | High | High |
| CSRF | High | High | High |
| XSS | High | High | High |
| Broken Access Control | Medium | Medium | High |

## Remediation priority

| Priority | Vulnerability | Rationale |
|---|---|---|
| 1 | SQL Injection | The most critical finding — allows full database access |
| 2 | Broken Authentication | The front door to the system; breaking it compromises the whole application |
| 3 | XSS | Directly targets regular users and leads to session theft |
| 4 | CSRF | Allows actions to be performed under a user's identity without their knowledge |
| 5 | Broken Access Control | Exposes server configuration, but needs to be combined with another flaw for full compromise |

## Risk distribution

| Risk level | Count | Share |
|---|---|---|
| Critical | 1 | 20% |
| High | 3 | 60% |
| Medium | 1 | 20% |
| Low | 0 | 0% |

## Overall assessment

**4 of 5 findings (80%) rate High or Critical.** This indicates Mutillidae
is, unsurprisingly for a deliberately vulnerable training app, in poor
security condition and entirely unsuitable for production use. The most
critical issue is SQL Injection, which alone can lead to full database
disclosure.
