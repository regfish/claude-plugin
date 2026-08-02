---
description: Full health check of a domain (reachability, mail, DNSSEC, web) via DNS Doctor, with concrete fixes.
argument-hint: <domain>
---

Run a full diagnosis for: $ARGUMENTS

Use `diagnose_domain`. Works on any domain, not only regfish customers'.

Report the score, then the findings sorted by what actually costs something:
mail delivery and reachability first, hardening second. For each real problem
name the concrete fix — the exact record to create or change, with host, type
and value.

Distinguish missing from wrong: a missing DMARC record is a gap, a `p=reject`
DMARC with a broken SPF is actively bouncing legitimate mail.

If the domain is in this account and a fix is obvious, offer to apply it — say
what you would change first, and verify afterwards.

If no domain was given, ask for one.
