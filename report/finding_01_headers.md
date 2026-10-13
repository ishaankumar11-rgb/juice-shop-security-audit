# Finding 1: Missing and weak HTTP security headers

- Severity: Low (my judgement, lab setting)
- Location: http://127.0.0.1:3000 (all responses)
- - Category: OWASP Top 10 2021, A05 Security Misconfiguration
- Evidence: evidence/01_headers.txt (`curl -sI`)
- - Steps to reproduce:
  1. Start the lab (docker command is in the main README).
  2. Run: `curl -sI http://127.0.0.1:3000`
  3. Read the response headers and compare with the list below.
- Observed:
  - Missing: Content-Security-Policy, Referrer-Policy, Permissions-Policy
  - Present but outdated: Feature-Policy (replaced by Permissions-Policy)
  - `Access-Control-Allow-Origin: *` allows any website to call the API from a browser
  - Extra header `X-Recruiting` discloses unnecessary information
- Impact: a missing CSP removes a defence layer against XSS; a wildcard CORS policy widens what other sites can do with the API.
- Fix: add a Content-Security-Policy, Referrer-Policy and Permissions-Policy; restrict CORS to trusted origins; remove non-essential headers.
- Note: HSTS is not applicable because the lab runs over plain HTTP on localhost.
