# Target Overview

## About the application

**OWASP Mutillidae II** is an intentionally vulnerable web application
built for practicing web security concepts and penetration testing. It
bundles a full set of common web vulnerabilities — SQL Injection, XSS,
Command Injection, Authentication Bypass, File Inclusion, and more —
behind a single navigable site, which makes it a good fit for a
structured assessment.

For this project, Mutillidae was run locally on Apache via XAMPP, with
all traffic routed through Burp Suite for inspection and manipulation.

## Application features relevant to this assessment

- Multiple user-input forms (login, search, feedback/blog)
- A toggle for the app's own internal "security level," useful for
  comparing behavior under weaker/stronger settings
- Direct, dynamic MySQL queries
- Cookie-based session management
- A module structure organized by vulnerability category

## User roles

**Anonymous user** — can reach public pages and submit data through
forms without logging in. Several vulnerabilities (reflected input,
unauthenticated access to sensitive pages) are reachable at this level
alone.

**Authenticated user** — logs in through the login form and gets access
to more of the application. This is where session-management and
access-control issues become relevant.

**Administrator** (simulated in some modules) — the target of
privilege-escalation attempts in several findings.

## Entry points

**Forms**

| Form | Endpoint | Related risks |
|---|---|---|
| Login | `index.php?page=login.php` | SQL Injection, Authentication Bypass |
| User lookup / search | `index.php?page=user-info.php` | SQL Injection, XSS |
| Blog / feedback | `index.php?page=add-to-your-blog.php` | XSS, HTML Injection |
| Registration | `index.php?page=register.php` | SQL Injection, XSS |

**Cookies**

| Cookie | Purpose | Related risks |
|---|---|---|
| `PHPSESSID` | Session management | Session Hijacking, Session Fixation |
| User preference cookies | Settings/preferences | Cookie manipulation |

**URL parameters**

| Parameter | Example | Related risks |
|---|---|---|
| `page` | `index.php?page=login.php` | Local/Remote File Inclusion |
| `id` | `?id=1` | SQL Injection, IDOR |

**HTTP headers**

| Header | Purpose | Related risks |
|---|---|---|
| `User-Agent` | Browser identification | Log poisoning, header injection |
| `Referer` | Request origin | Referer spoofing |

**HTTP methods**

| Method | Purpose | Related risks |
|---|---|---|
| GET | Retrieving data | Parameter tampering |
| POST | Form submission | SQL Injection, XSS |

## Attack surface summary

- Numerous user-input forms
- Mutable URL parameters
- Session cookies
- HTTP requests that can be freely intercepted and modified
- Direct, unparameterized MySQL access from application code
