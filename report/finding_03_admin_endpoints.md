# Finding 3: Administrative endpoints respond without authentication

- Severity: Medium (my judgement, lab setting)
- Location: http://127.0.0.1:3000/rest/admin/application-version and /rest/admin/application-configuration
- Evidence: evidence/03_admin_version.json, evidence/03_admin_config.json (HTTP 200, no login, no token)
- Observed:
  - application-version returns the exact version (20.2.0)
  - application-configuration returns a large JSON document (about 24 KB) with sections: server, application, challenges, hackingInstructor, products, memories, ctf
- Note: I listed only section names and searched key names for words like key, secret, password, token. No credential-like keys were found. I did not review or copy values.
- Impact: an unauthenticated visitor learns the exact software version (useful for finding known vulnerabilities) and how the application is configured. Paths containing "admin" should never be reachable without authorization.
- Fix: require authentication and an admin role on every /rest/admin route; return 401 or 403 otherwise; do not expose version or configuration publicly.
- Reference: OWASP Top 10 A01 Broken Access Control, A05 Security Misconfiguration
