---
description: Look at regfish web hosting packages and connect them with DNS — which package a domain runs on, which databases and aliases exist, and why a domain does not reach its hosting. Use when the question involves web hosting, a package, a website that does not come up, shows a white page or the wrong site, PHP versions, databases, or pointing a domain at hosting — including after a DNS change that should have moved the site. In German: Website ist weg, weiße Seite, Seite lädt nicht.
---

# Web hosting at regfish

The hosting tools are **read-only**. There is no tool to book, upgrade, cancel
or restore anything — those cost money or are irreversible and stay in the
regfish dashboard. Say that plainly when someone asks for them instead of
looking for a workaround.

## The four tools

`list_hosting_packages` gives the overview: plan, status, PHP version, how many
aliases and databases each package has. Everything else needs the package `id`
from that list.

`get_hosting_package` adds detail for one package, including whether a backup
recovery is currently running.

`list_hosting_aliases` shows which domains are attached to a package, and
whether each has its own vHost or shares the main one.

`list_hosting_databases` lists databases with name, user and host —
**never passwords**. The API does not return them at all, so do not promise to
look them up. Point at the dashboard.

## The question that comes up most: "my domain doesn't show my website"

That is almost always one of two things, and they are diagnosed differently:

1. **The domain is not attached to the package.** Check
   `list_hosting_aliases` — if the domain is not in that list, hosting never
   sees the request. Attaching it is a dashboard action.
2. **The domain is attached, but DNS points elsewhere.** Check
   `list_dns_records` for the zone: does the A record (and AAAA, if present)
   point at the hosting? Compare against a domain on the same package that
   works. Then `check_dns_propagation` to see whether a recent change has
   actually reached the resolvers, and `diagnose_domain` for the full picture.

Do both checks before proposing a change. Editing DNS when the alias is missing
fixes nothing, and attaching an alias when DNS points at an old server fixes
nothing either.

## Reading the state honestly

`status` and `active` are not the same thing: a package can exist and be
inactive. A `cancelled` package still serves until it expires — say when that
is, do not report it as gone.

A running backup recovery (`backup.recover_status`) explains a lot of odd
behaviour. Check it before hunting for other causes, and do not start changing
DNS while a restore is in flight.

## PHP

The PHP version is visible per package but not changeable here. If a site needs
a different version, that is a dashboard action — and worth a warning, because
switching PHP versions can break a site that relies on the old one.
