# regfish for Claude Code

Manage your [regfish](https://regfish.de) domains, DNS records, DNSSEC and web
hosting directly from Claude — with one install, not three.

```shell
claude plugin marketplace add regfish/claude-plugin
claude plugin install regfish@regfish --config api_key=<your-api-key>
```

Your key goes into the install command and is stored in the system keychain, not
in a config file.

**Then start a new session.** Commands and MCP servers are wired up when a
session starts, so a session that was already running does not see the plugin
yet — `/reload-plugins` inside it, or simply open a new one.

The same two lines work as `/plugin …` inside a running session. If you leave
`--config` off, the plugin installs but stays unconfigured, and the tools answer
with a 401 that says so — rerun the install command with the key, or use
`/plugin configure regfish@regfish` where the interactive dialog is available.

Written literally, the key lands in your shell history. To avoid that, keep it in
a file and let the shell substitute it:

```shell
printf %s '<your-api-key>' > ~/.regfish-api-key && chmod 600 ~/.regfish-api-key
claude plugin install regfish@regfish --config api_key="$(cat ~/.regfish-api-key)"
```

## What you get

The plugin bundles three things that are usually configured separately:

| | What it is | What it does here |
|---|---|---|
| **MCP server** | The connection to regfish | 29 tools for domains, DNS, DNSSEC, diagnostics and hosting |
| **Skills** | Working knowledge | Teaches Claude *how* to work here: read before write and verify after for DNS, how to read a diagnosis, how hosting and DNS fit together — and to answer regfish questions from the official knowledge base instead of guessing |
| **Plugin** | The package | Ships both, versioned and updatable |

Without the skills, Claude has tools but no judgement about them: it might add
a second SPF record instead of updating the first, or report a queued DNSSEC
job as finished. The skills are the difference between "it can call the API"
and "you can let it work".

## The API key

Create one in the regfish dashboard under **Settings → Security → API keys**.

Pick a role that matches the job — that is enforced server-side, not just in
Claude:

| Role | Claude can |
|---|---|
| Read only | look at everything, change nothing |
| DNS administrator | read plus create, change and delete DNS records |
| Domain management | additionally switch nameservers and request auth codes |
| Full access | everything the API offers |

A key with a role only ever sees the tools it may use. Give an assistant the
narrowest role that gets the job done.

## Examples

```
> list my dns zones
> add an A record for staging.example.de pointing at 203.0.113.10
> why is mail for example.de landing in spam?
> check whether my nameserver change has propagated
> is DNSSEC actually active for example.de?
> which hosting package is example.de running on?
> why doesn't my domain show my website?
```

## What it will not do

Registering, transferring and cancelling domains are not available through the
API by design — they cost money, involve deadlines and cannot be undone by
retrying. Those stay in the dashboard.

Database passwords and other secrets are never returned by the API, so Claude
cannot leak them.

## Documentation

* Setup, tool catalog and security model: <https://regfish.de/docs/mcp>
* DNS API reference: <https://regfish.de/docs>
* Diagnostics API: <https://regfish.de/docs/dns-doctor>

## Without Claude Code

The MCP server works with any MCP client. Point it at
`https://api.regfish.com/mcp` with `Authorization: Bearer <your-api-key>`.
See the documentation linked above for a ready-made configuration snippet.

## Also in this marketplace

`dns-doctor@regfish` — free DNS, mail and security checks against any domain, no
account needed. Lives in [regfish/dns-doctor-mcp](https://github.com/regfish/dns-doctor-mcp)
and installs from here:

```shell
claude plugin install dns-doctor@regfish
```

## License

MIT — see [LICENSE](LICENSE).
