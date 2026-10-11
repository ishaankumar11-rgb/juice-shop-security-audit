# Finding 1: Missing and weak HTTP security headers

- Severity: Low (my judgement, lab setting)
- Location: http://127.0.0.1:3000 (all responses)
- Evidence: evidence/01_headers.txt (`curl -sI`)
- Observed:
  - Missing: Content-Security-Policy, Referrer-Policy, Permissions-Policy
  - Present but outdated: Feature-Policy (replaced by Permissions-Policy)
  - `Access-Control-Allow-Origin: *` allows any website to call the API from a browser
  - Extra header `X-Recruiting` discloses unnecessary information
- Impact: a missing CSP removes a defence layer against XSS; a wildcard CORS policy widens what other sites can do with the API.
- Fix: add a Content-Security-Policy, Referrer-Policy and Permissions-Policy; restrict CORS to trusted origins; remove non-essential headers.
- Note: HSTS is not applicable because the lab runs over plain HTTP on localhost.
