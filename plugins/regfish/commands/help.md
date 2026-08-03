---
description: Answer a regfish question from the official knowledge base (help center, procedures, legal, developer docs), with the source linked.
argument-hint: <question>
---

Answer this regfish question: $ARGUMENTS

Use `search_help` with the question as given. Answer from the excerpts, in the
user's language, and link the article URL as the source.

Keep product UI labels exactly as the articles spell them („Mein Vertrag",
„AuthInfo einblenden") — that is what the customer sees on screen. Do not
paraphrase menu or button names, and do not invent steps the articles do not
mention.

If the search returns nothing, say the knowledge base has nothing on this and
point to support@regfish.com. Never answer a regfish process question from
general registrar knowledge — the details differ, and a made-up click path is
worse than none.

If the question also touches this account's own data ("is my transfer lock
on?"), combine: `search_help` for the process, the account tools
(`get_domain`, `list_dns_records`, …) for the current state.
