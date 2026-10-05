# RabTech Task 2 – Accessibility Audit

## Project Overview

This project contains an accessibility and repository architecture audit of the National Portal of India.

## Website Audited

- **Website:** National Portal of India
- **URL:** https://www.india.gov.in/
- **Audit Tool:** Google Lighthouse
- **Manual Test:** Keyboard-only navigation
- **Audit Type:** Accessibility and basic architecture review

## Lighthouse Results

| Category | Score |
|---|---:|
| Performance | 70 |
| Accessibility | 88 |
| Best Practices | 92 |
| SEO | 100 |

## Accessibility Findings

The audit identified issues including:

- ARIA child roles not contained by required parent elements
- Focusable elements inside `aria-hidden="true"` elements
- Insufficient color contrast
- Missing main landmark
- Other accessibility improvements identified by Lighthouse

## Repository Structure

```text
rabtech-task-2-accessibility-audit/
├── client/
├── server/
├── test/
├── docs/
│   ├── screenshots/
│   └── audit-report.md
└── README.md
