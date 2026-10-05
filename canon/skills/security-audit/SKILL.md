---
name: security-audit
description: Mandatory pre-handoff pass for OWASP-style issues (injection, access control, XSS, data exposure); fixes obvious problems in-tree and flags residual risk. Use after generating or materially editing security-sensitive code.
---

# Security audit

- After substantive code generation or security-relevant edits, perform a focused **security scan** using **OWASP Top 10** style checks (injection, broken access control, XSS, sensitive data exposure, misconfiguration, etc.).
- **Pre-exposure & perimeter checks:** Prior to configuring public routing (Cloudflare Tunnels, reverse proxies, ingress, port forwarding), ensure initial setup wizards or unauthenticated admin onboarding endpoints are not exposed to the public internet, and state perimeter boundaries explicitly in advance.
- Correct clear issues in the same change set; document any remaining risk that requires human review or policy decisions.
