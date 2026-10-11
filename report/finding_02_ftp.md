# Finding 2: Unauthenticated directory listing exposes internal files

- Severity: High in a real application (my judgement, lab setting)
- Location: http://127.0.0.1:3000/ftp
- Evidence: screenshots/02_ftp_listing.png, evidence/02_ftp_listing.html, evidence/02_ftp_filenames.txt
- Observed: the /ftp path returns HTTP 200 without any login and lists 10 files and one folder (quarantine), including:
  - backup files: coupons_2013.md.bak, package.json.bak, package-lock.json.bak
  - a file named incident-support.kdbx (a KeePass password database format)
  - internal-looking documents: acquisitions.md, announcement_encrypted.md, suspicious_errors.yml
  - compiled code: encrypt.pyc
- Note: I did not open or download any of these files. The impact below is based on file names and types only.
- Impact: anyone who can reach the app can see internal file names and likely fetch them. Backup and dependency files can reveal software versions and secrets; a password database or internal documents would be a serious data leak.
- Fix: disable directory listing; remove backups and internal documents from the web root; require authentication for any file area; store secrets outside the application.
- Reference: OWASP Top 10 A01 Broken Access Control
