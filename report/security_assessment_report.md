# Security Assessment Report: OWASP Juice Shop (lab)

Arrowstack Cyber Security Internship, Task 3 (optional).

## 1. Executive summary
I assessed OWASP Juice Shop, an intentionally vulnerable training app, running in a Docker container on my own Kali VM. I found 4 issues: 1 High (DOM XSS), 1 High (open directory listing), 1 Medium (unauthenticated admin endpoints) and 1 Low (weak HTTP headers). Details, evidence and fixes are in `report/finding_*.md`.

## 2. Scope and authorization
See `report/scope.md`. Only http://127.0.0.1:3000 on my own VM was tested. The container was bound to localhost so it was not reachable from any network.

## 3. Method
1. Reviewed HTTP response headers with curl
2. Browsed the app through Burp Suite Community and reviewed HTTP history for unusual endpoints
3. Checked suspicious paths (/ftp, /rest/admin/...) for access control with read-only requests
4. Tested the search box with one harmless XSS test input
Files were listed but not opened or downloaded; configuration values were not reviewed.

## 4. Findings summary
| # | Finding | Severity | OWASP Top 10 | Evidence |
|---|---------|----------|--------------|----------|
| 1 | Missing and weak HTTP security headers | Low | A05 | evidence/01_headers.txt |
| 2 | Unauthenticated directory listing at /ftp | High | A01 | screenshots/02_ftp_listing.png |
| 3 | Admin endpoints respond without authentication | Medium | A01, A05 | evidence/03_admin_*.json |
| 4 | DOM-based XSS in the search box | High | A03 | screenshots/04_xss_alert.png |

Severity is my own judgement for a lab setting, not a formal CVSS score.

## 5. Remediation priorities
1. Fix XSS: encode output, never insert user input as raw HTML (Finding 4)
2. Remove directory listing and move backups and internal documents out of the web root (Finding 2)
3. Require authentication and an admin role on all /rest/admin routes (Finding 3)
4. Add CSP, Referrer-Policy and Permissions-Policy; restrict CORS (Finding 1)

## 6. Limitations
- A training app that is deliberately vulnerable, so these results are not a measure of real-world risk.
- Limited, manual testing: 4 areas, no automated scan, no authenticated testing.
- Fixes were recommended but not applied or re-tested.
- The Juice Shop version was 20.2.0 at the time of testing.
