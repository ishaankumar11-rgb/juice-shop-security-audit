# Juice Shop Security Audit

Arrowstack Cyber Security Internship, Task 3 (optional/bonus). A small web application security assessment of OWASP Juice Shop in my own lab.

## Read first
- `report/security_assessment_report.md` : summary and priorities
- `report/finding_01..04_*.md` : each finding with evidence, impact and fix
- `report/scope.md` : scope and authorization

## Lab setup
    sudo docker run -d --name juice-shop -p 127.0.0.1:3000:3000 bkimminich/juice-shop

The app is bound to localhost only. Tools: Firefox, Burp Suite Community, curl.

## Ethics
Only my own lab was tested. Never run these tests against systems you do not own or have written permission to test.
