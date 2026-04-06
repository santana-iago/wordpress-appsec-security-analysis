# Testing Methodology

## Overview

This assessment was conducted using a controlled black-box approach, simulating an external attacker without privileged access. The goal was to identify potential vulnerabilities, validate real exploitability, and analyze the application’s defensive mechanisms.

The methodology combined manual testing techniques with automated tools to evaluate the attack surface and security controls of the application.

---

## Reconnaissance and Information Gathering

Initial reconnaissance focused on identifying exposed endpoints and technologies in use.

### Techniques used:
- Inspection of HTTP requests via browser DevTools
- Enumeration of WordPress-specific endpoints
- Analysis of publicly accessible resources

### Key targets:
- WordPress REST API (`/wp-json`)
- Author enumeration (`/?author=ID`)
- HTML metadata exposure

---

## User Enumeration Testing

User enumeration was tested through multiple vectors:

### Methods:
- Direct requests to:
  - `/wp-json/wp/v2/users`
- Enumeration via:
  - `/?author=ID`
- Automated discovery using WPScan

### Objective:
To determine whether valid usernames could be identified without authentication.

---

## Authentication Testing

Authentication mechanisms were tested to evaluate response behavior and resistance to enumeration.

### Methods:
- XML-RPC authentication attempts using:
  - `wp.getUsersBlogs`
- Comparison between:
  - valid usernames
  - invalid usernames

### Objective:
To verify whether the system differentiates responses and leaks information about valid users.

---

## XML-RPC Analysis

The XML-RPC endpoint was analyzed for potential abuse.

### Methods:
- Verification of XML-RPC availability (`/xmlrpc.php`)
- Enumeration of available methods
- Testing of:
  - `system.multicall`

### Objective:
To assess whether multiple authentication attempts could be executed in a single request (brute-force amplification).

---

## Rate Limiting Evaluation

Rate limiting controls were tested to determine their effectiveness.

### Methods:
- Repeated authentication attempts
- Observation of lockout behavior
- Analysis of error responses and cooldown periods

### Objective:
To evaluate whether brute-force attacks are mitigated.

---

## WAF and Protection Mechanism Analysis

The presence and behavior of upstream protection mechanisms were evaluated.

### Methods:
- Analysis of HTTP headers
- Identification of Cloudflare
- Testing of blocked requests (HTTP 403)
- Response time measurement

### Objective:
To determine whether malicious requests are intercepted before reaching the application.

---

## Plugin and CVE Validation

Known vulnerabilities identified via WPScan were manually validated.

### Identified vulnerabilities:
- CVE-2024-8200 (CSRF)
- CVE-2024-8199 (Authorization bypass)

### Methods:
- Inspection of AJAX endpoints (`admin-ajax.php`)
- Manual crafting of requests using curl
- Attempted access to plugin-related actions

### Objective:
To verify whether vulnerabilities are exploitable in the current environment.

---

## AJAX Endpoint Testing

AJAX functionality was analyzed to identify exposed backend actions.

### Methods:
- Monitoring network traffic via DevTools
- Filtering requests for:
  - `admin-ajax.php`
- Manual testing of potential actions

### Objective:
To identify unauthenticated access to backend functionality.

---

## Tools Used

- WPScan (WordPress vulnerability scanner)
- curl (manual HTTP request testing)
- Browser DevTools (network inspection)
- Linux environment (command-line testing)

---

## Approach Summary

The assessment followed a practical, attack-oriented methodology focused on:

- identifying exposed attack surfaces
- validating real-world exploitability
- correlating application behavior with security controls

The goal was not only to detect vulnerabilities, but to determine whether they could be effectively exploited under realistic conditions.
