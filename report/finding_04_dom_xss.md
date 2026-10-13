# Finding 4: DOM-based cross-site scripting (XSS) in the search box

- Severity: High in a real application (my judgement, lab setting)
- Location: http://127.0.0.1:3000/#/search?q=<payload>
- Evidence: screenshots/04_xss_alert.png
- Test input (harmless, only shows a message box): <iframe src="javascript:alert('xss')">
- Steps to reproduce:
  1. Start the lab (docker command is in the main README).
  2. Open http://127.0.0.1:3000 in Firefox.
  3. Paste the test input above into the search box and submit.
  4. A browser alert showing "xss" appears (see screenshots/04_xss_alert.png).
- Observed: after submitting the input in the search box, a browser alert showing "xss" appeared, so the application inserted user-controlled text into the page and the browser ran it as code.
- Impact: in a real app an attacker could send a victim a crafted link and run script in the victim's session (steal session data, act as the victim, change page content).
- Fix: do not insert user input as raw HTML; encode output; avoid bypassing the framework's sanitiser; add a Content-Security-Policy (see Finding 1).
- Reference: OWASP Top 10 A03 Injection
