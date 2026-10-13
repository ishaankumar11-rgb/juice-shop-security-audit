# Juice Shop Security Audit

Arrowstack Cyber Security Internship, Task 3 (optional/bonus). A small web application security assessment of OWASP Juice Shop in my own lab.

## Read first
- `report/security_assessment_report.md` : summary and priorities
- `report/finding_01..04_*.md` : each finding with evidence, impact and fix
- `report/scope.md` : scope and authorization
  
## Findings at a glance

4 findings: 2 High, 1 Medium, 1 Low. Severity is my own judgement for a lab setting, not a formal CVSS score.

| # | Finding | Severity | OWASP Top 10 | Details |
|---|---------|----------|--------------|---------|
| 1 | Missing and weak HTTP security headers | Low | A05 | [finding_01](report/finding_01_headers.md) |
| 2 | Unauthenticated directory listing at /ftp | High | A01 | [finding_02](report/finding_02_ftp.md) |
| 3 | Admin endpoints respond without authentication | Medium | A01, A05 | [finding_03](report/finding_03_admin_endpoints.md) |
| 4 | DOM-based XSS in the search box | High | A03 | [finding_04](report/finding_04_dom_xss.md) |
## Lab setup
    sudo docker run -d --name juice-shop -p 127.0.0.1:3000:3000 bkimminich/juice-shop

The app is bound to localhost only. Tools: Firefox, Burp Suite Community, curl.

## Ethics
Only my own lab was tested. Never run these tests against systems you do not own or have written permission to test.
