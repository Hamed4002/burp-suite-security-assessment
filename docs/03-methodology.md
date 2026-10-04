# Methodology

## Tools

**XAMPP** — a free, open-source package bundling Apache, MySQL, PHP, and
Perl. Used to host Mutillidae locally, giving a fully isolated,
internet-independent environment for testing.

**Firefox** — the primary browser, chosen for its straightforward manual
proxy configuration and developer tooling. All browser traffic was routed
through Burp Suite for inspection.

**Burp Suite** — the core tool of this project, developed by PortSwigger.
It sits as a proxy between the browser and the server, allowing every
HTTP/HTTPS request and response to be intercepted, inspected, and
modified. The free Community Edition provided: live request/response
interception, request modification before forwarding, request replay with
arbitrary changes, automated attacks with payload lists, and site-structure
analysis.

**Mutillidae II** — the target application (see
[`01-target-overview.md`](01-target-overview.md)), served from
XAMPP's `htdocs`.

## Test environment setup

**1. Proxy configuration in Firefox**

- In Burp Suite's Proxy tab, confirmed the proxy listener on `127.0.0.1:8080`
- In Firefox's proxy settings: HTTP Proxy `127.0.0.1`, Port `8080`, with "Also use this proxy for HTTPS" enabled

**2. Installing Burp's SSL certificate**

Even though Mutillidae is served over plain HTTP on localhost, the CA
certificate was installed anyway (relevant for any HTTPS target):

- Opened `http://burp` in the browser, downloaded the CA certificate
- Imported it in Firefox via Settings → Privacy & Security → View Certificates → Import

**3. Enabling Intercept**

Turned on "Intercept is on" under the Proxy tab so each request could be
reviewed and modified before it reached the server.

## Burp Suite tools used

| Tool | Purpose | How it was used here |
|---|---|---|
| Proxy | Intercept/modify requests | Inspect and tamper with parameters sent to the server |
| Target | Site map | Identify the site's structure and entry points |
| Repeater | Resend requests with changes | Test different SQLi/XSS payloads |
| Intruder | Automated attacks with payload lists | Brute-force style testing |
| Decoder | Encode/decode data | Analyze encoded cookies and parameters |
| Comparer | Diff responses | Spot differences useful for blind-style attacks |

## Testing cycle

**Step 1 — Mapping**
With Intercept off, browse the site normally; use Target → Site map to
enumerate pages; note down the important entry points (forms, URL
parameters, cookies).

**Step 2 — Intercepting and analyzing requests**
Turn Intercept on, submit various forms, and examine each HTTP request's
method, parameters, headers, and cookies to understand its structure.

**Step 3 — Documenting evidence**
Save each successful request/response pair under Proxy → HTTP history,
capture the necessary screenshots, and record working payloads separately.
