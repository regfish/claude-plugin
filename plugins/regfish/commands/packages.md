---
description: List the regfish hosting packages in this account and which domains run on them.
argument-hint: [package-id]
---

Show the hosting situation$ARGUMENTS

Without an argument: use `list_hosting_packages` and give an overview — plan,
status, PHP version, how many aliases and databases each package has.

With a package id: use `get_hosting_package`, `list_hosting_aliases` and
`list_hosting_databases` for the detail. Never promise database passwords; the
API does not return them.

Flag anything that explains trouble: a cancelled package still serving until it
expires (say when), an inactive package, a backup recovery in progress.

These tools are read-only. Booking, upgrading and cancelling stay in the
dashboard.
