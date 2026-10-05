# Accessibility & Repository Architecture Audit

## 1. Website Audited

- **Website:** National Portal of India
- **URL:** https://www.india.gov.in/
- **Audit Tool:** Google Lighthouse
- **Manual Test:** Keyboard-only navigation
- **Audit Type:** Accessibility and basic architecture review

---

## 2. Lighthouse Baseline

| Category | Score |
|---|---:|
| Performance | 70 |
| Accessibility | 88 |
| Best Practices | 92 |
| SEO | 100 |

---

## 3. Accessibility Findings

### Finding 1 — Incorrect ARIA Parent-Child Relationships

**Severity:** High  
**Source:** Lighthouse

Lighthouse reported:

`[role] elements are not contained by their required parent element`

The audit identified an affected element associated with:

`#topBarServiceList`

**Impact:** Incorrect ARIA hierarchy can prevent assistive technologies from interpreting the interface correctly.

**Recommended remediation:** Review the ARIA roles used around `#topBarServiceList`. Ensure child roles are placed inside their required parent roles, or replace unnecessary ARIA with appropriate semantic HTML.

---

### Finding 2 — Focusable Descendants Inside aria-hidden

**Severity:** High  
**Source:** Lighthouse

Lighthouse reported:

`[aria-hidden="true"] elements contain focusable descendants`

Multiple service and trending elements were identified by the audit.

**Impact:** Keyboard-focusable content inside an `aria-hidden="true"` container may remain keyboard accessible while being unavailable to screen readers, creating an inconsistent experience.

**Recommended remediation:** Remove `aria-hidden="true"` when the content should be accessible, or ensure hidden containers do not contain focusable interactive elements.

---

### Finding 3 — Insufficient Color Contrast

**Severity:** Medium-High  
**Source:** Lighthouse

Lighthouse reported:

`Background and foreground colors do not have a sufficient contrast ratio.`

Affected content included service-category and service-carousel text such as:

- Central Government
- State Government
- Important Service
- Information Categories

**Impact:** Low-contrast text can be difficult to read, particularly for users with low vision or color-vision deficiencies.

**Recommended remediation:** Increase foreground/background contrast and verify the resulting contrast against the applicable WCAG requirements.

---

### Finding 4 — Missing Main Landmark

**Severity:** Medium-High  
**Source:** Lighthouse

Lighthouse reported:

`Document does not have a main landmark.`

The audit identified the document as the affected element.

**Impact:** Screen-reader users benefit from a main landmark for quickly navigating to the primary page content.

**Recommended remediation:** Add a semantic `<main>` element around the primary content of the page.

---

### Finding 5 — Failed Resource Requests

**Severity:** Medium  
**Source:** Chrome DevTools Console

The browser console recorded multiple failed resource requests during the audit, including:

- HTTP 503 — Service Unavailable
- HTTP 404 — Not Found

A separate `ERR_BLOCKED_BY_CLIENT` message was also observed but was not treated as a confirmed website defect because browser extensions can cause this type of error.

**Impact:** Failed resource requests can cause missing functionality or incomplete page resources.

**Recommended remediation:** Identify the affected endpoints/resources, verify server availability and routing, and monitor recurring 4xx/5xx errors.

---

## 4. Keyboard-Only Navigation Test

A manual keyboard-only navigation test was performed using:

- `Tab`
- `Shift + Tab`

### Result: PASS

Interactive elements were reachable through sequential keyboard navigation. Reverse navigation using `Shift + Tab` also worked normally.

No obvious keyboard focus trap or unexpected focus jump was observed during the test.

---

## 5. Summary

The audit identified five issues requiring remediation:

1. Incorrect ARIA parent-child relationships
2. Focusable descendants inside `aria-hidden="true"`
3. Insufficient color contrast
4. Missing main landmark
5. Failed resource requests

The keyboard-only navigation test passed without an obvious focus-trap issue.

---

## 6. Repository Architecture

```text
rabtech-task-2-accessibility-audit/
├── client/
├── server/
├── docs/
│   ├── audit-report.md
│   └── screenshots/
└── test/
