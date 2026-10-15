# FUTURE_CS_01: Vulnerability Assessment

**Future Interns Cyber Security Internship, Task 1**
**Author:** Midhat Zaidi

## Overview
This task is a passive, read-only vulnerability assessment of a public test server. I looked for common security weaknesses, rated how serious each one is, and wrote down a fix for each. Nothing was exploited.

## Target
- **Host:** scanme.nmap.org (45.33.32.156)
- **Why this site:** it is run by the Nmap project and is open for scan practice
- **Assessment type:** passive, no logins, no exploitation, no brute force
- **Also scanned:** testphp.vulnweb.com. All 100 checked ports came back filtered, so it produced no findings.

## Tools Used
- **Nmap**: port and service discovery
- **OWASP ZAP (Safe Mode)**: passive web security scan
- **Browser DevTools**: HTTP response header review

## Methodology
1. **Nmap:** ran `nmap -Pn -sV --top-ports 100 scanme.nmap.org` to find open ports and service versions.
2. **OWASP ZAP:** explored the site through ZAP in Safe Mode and reviewed the passive alerts.
3. **DevTools:** checked the response headers in Chrome for missing security headers.
4. **Report:** rated each finding and wrote a recommended fix.

## Nmap Results
| Port | State | Service |
|------|-------|---------|
| 22/tcp | Open | SSH, OpenSSH 6.6.1p1 |
| 80/tcp | Open | HTTP, Apache 2.4.7 |
| 25/tcp | Filtered | SMTP |
| 1720/tcp | Filtered | H.323 |
| 5060/tcp | Filtered | SIP |

## Summary of Findings
9 findings: 6 Medium, 2 Low, 1 Informational.

| # | Finding | Risk |
|---|---------|------|
| 1 | No HTTPS | Medium |
| 2 | Older web server (Apache 2.4.7) | Medium |
| 3 | Older SSH service (OpenSSH 6.6.1) open to the internet | Medium |
| 4 | No Content Security Policy | Medium |
| 5 | No anti-clickjacking protection | Medium |
| 6 | Outside scripts not integrity-checked | Medium |
| 7 | Server header reveals its exact version | Low |
| 8 | Missing X-Content-Type-Options header | Low |
| 9 | Unused ports blocked by firewall (good practice) | Informational |

## What to Fix First
1. Enable HTTPS and redirect all traffic to it.
2. Update Apache and OpenSSH, and limit SSH to trusted addresses.
3. Add the missing security headers and hide the Server version.

## Files in This Repository
- `Vulnerability_Assessment_Report.pdf`: the full report
- `nmap_scanme.jpeg`, `scanme_scan.txt`: Nmap scan screenshot and output
- `testphp_scan.txt`: scan output for the second site
- `headers_scanme.jpeg`: DevTools response headers
- `zap_alerts_1.png` to `zap_alerts_4.png`: OWASP ZAP alert screenshots
- `zap_csp_detail.png`, `zap_server_detail.png`: ZAP alert details

## Disclaimer
Only sites that allow security testing were scanned. This work was done for learning purposes.
