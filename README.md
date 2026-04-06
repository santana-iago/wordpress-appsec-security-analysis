# WordPress Application Security Assessment

## Overview
This project documents a controlled application security assessment performed against a WordPress-based web application, focusing on authentication, XML-RPC exposure, public API exposure, and plugin-related risks.

## Scope
- Authentication flows
- XML-RPC endpoint
- WordPress REST API
- Public user exposure
- Known plugin CVEs
- WAF and rate-limiting behavior

## Methodology
The assessment was conducted using a black-box approach with authorized testing, combining:
- WPScan
- curl
- browser DevTools
- manual HTTP analysis
- controlled proof-of-concept testing

## Key Findings
- User enumeration via public WordPress endpoints
- XML-RPC enabled but protected by WAF
- Strong rate limiting behavior
- No practical exploitation identified for known plugin CVEs
- Authentication flow did not allow username enumeration

## Tools Used
- WPScan
- curl
- Google Chrome DevTools

## Outcome
The assessment identified moderate information exposure risks, mainly related to public user enumeration, while critical attack paths such as XML-RPC multicall abuse and brute-force amplification were effectively mitigated by rate limiting and WAF protections.

## Report
The full case study is available in the repository as a PDF titled Application_Security_Assessment_Report

## Learning Goals
This project was developed as part of an AppSec learning path focused on:
- vulnerability validation
- attack surface analysis
- secure interpretation of findings
- technical reporting
