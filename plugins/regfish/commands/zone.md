---
description: Show all DNS records of a regfish zone, grouped and readable, with anything unusual called out.
argument-hint: <domain>
---

Show the DNS zone for: $ARGUMENTS

Use `list_dns_records`. Present the records grouped by type, not as a raw dump:
apex records first, then subdomains, then mail (MX, SPF, DKIM, DMARC), then
everything else. Include the TTL and the record id, because the id is what a
later change needs.

Point out anything that looks off — a second SPF record, an MX with no A record
behind it, a CNAME next to other records at the same name, a TTL so low it
suggests an unfinished migration. Do not change anything; this command only
reads.

If no domain was given, run `list_dns_zones` and ask which one.
