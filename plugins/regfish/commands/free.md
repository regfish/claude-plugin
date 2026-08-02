---
description: Check whether a domain is still registrable, using the regfish registry lookup.
argument-hint: <domain>
---

Check availability for: $ARGUMENTS

Use `check_domain_available`. Report the plain answer first, then the detail:

- `available` — registrable right now.
- `redemption_period` or `pending_delete` — taken today, but on its way back to
  the market. Say that explicitly, it changes what the customer does next.
- `reserved` — the registry blocks it. Waiting will not help.
- `registered` — taken, no scheduled release.

If the check fails, say the check did not go through and offer to retry. Never
turn an error into "not available".

If `premium_class` is set, mention the domain is a registry premium name and
that pricing differs — but do not quote the class as a price.

Registration itself is not available through the API; the next step is the
regfish dashboard.

If several domains were given, check them all and answer as a short list.
