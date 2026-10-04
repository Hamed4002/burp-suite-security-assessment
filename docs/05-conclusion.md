# Conclusion

## Project summary

This project carried out a security assessment of the vulnerable web
application Mutillidae II, using Burp Suite and taking on the role of a
security analyst. The main goals were to identify common web
vulnerabilities, understand their root causes, and propose concrete
secure-coding remediations.

## Findings summary

| Vulnerability | Risk Level | OWASP Top 10 (2021) category |
|---|---|---|
| SQL Injection | Critical | A03: Injection |
| Broken Authentication | High | A07: Identification and Authentication Failures |
| CSRF | High | Not a standalone category since 2017 — conceptually under A01: Broken Access Control (CWE-352) |
| XSS | High | A03: Injection |
| Broken Access Control | Medium | A01: Broken Access Control |

4 of 5 findings (80%) rate High or Critical, and four map directly to
a current OWASP Top 10 category; the fifth (CSRF) remains a
well-documented risk (CWE-352) even though it's no longer broken out on
its own in the 2021 list.

## Lessons learned

**1. Input validation matters everywhere.**
Every vulnerability found traces back to the application trusting user
input where it shouldn't. Both SQL Injection and XSS occur purely because
input is never validated or sanitized.

**2. Authorization has to be enforced server-side.**
The broken access control finding showed that permission checks must
happen on the server — hiding a link in the UI is not a security
boundary.

**3. A half-implemented security mechanism can be worse than none.**
The CSRF finding showed that merely *having* a token field isn't enough —
an unvalidated token creates a false sense of security without providing
any actual protection.

**4. Session and authentication hygiene is foundational.**
Weak authentication (no rate limiting, information-leaking error
messages) opens the door to brute-force attacks and account takeover.

## Final recommendations

**For developers:**
- Never trust user input — validate everything, and prefer whitelisting over blacklisting
- Use prepared statements to eliminate SQL injection at the root
- Sanitize output (e.g. `htmlspecialchars`) to prevent XSS
- Enforce authorization checks server-side on every sensitive request
- Implement security mechanisms completely — a CSRF token must be generated, stored, *and* validated

**For organizations:**
- Run regular penetration tests against web applications
- Train development teams on secure coding and the OWASP Top 10
- Prefer modern frameworks, which implement many of these protections by default

## Closing note

Mutillidae is an excellent learning environment for understanding web
vulnerabilities. This project demonstrated how insecure coding practices
can lead to serious consequences — data leaks, session theft, and
unauthorized access — and how a handful of well-understood, not
particularly complex secure-coding principles would have prevented every
single finding in this report.
