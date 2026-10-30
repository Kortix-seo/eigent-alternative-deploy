# Open source Eigent alternative deploy template

Kortix is open source, and this repository is a working deploy template for running a company-wide agent platform as an open-source alternative to Eigent. Clone it, read the two config files, and bring the open-source CompanyOS up on a machine you control.

Kortix is the open-source CompanyOS: your agents, their skills, your company memory, and every connector live in one git repo you own, and every session runs on its own cloud computer. [Eigent](https://github.com/eigent-ai/eigent) is an open-source Cowork desktop. Its own repository calls it "the open source Cowork desktop application" and ships it as a local-first desktop app for macOS, Windows and Linux, built on CAMEL-AI's multi-agent framework. Eigent keeps agents on each person's machine; Kortix runs the same agents on isolated cloud computers a whole company shares, scopes and governs from one repo.

## What is in this repository

- `kortix.yaml` is a valid v2 manifest with one agent and two triggers. It declares the agent, the connectors and secrets that agent may reach, and the schedules that start its work.
- `agents/ops-agent.md` is the agent the manifest names. Behavior lives in the markdown file; governance lives in `kortix.yaml`.
- `docker-compose.yml` is a readable mirror of the self-host stack: the frontend, the API, the LLM gateway, and the Supabase distribution, so you can see the shape of what runs.
- `docs/` holds three articles, linked in the Docs section below.

## Quick start

The supported install is three commands on a Linux box you control. Install the CLI, initialize the instance, then start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Point an A/AAAA record for your domain and for `api.<domain>` at the box's IP before you initialize, and open ports 80 and 443 so the bundled Caddy proxy can issue a TLS certificate. To try Kortix with no domain, use the evaluation mode instead:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use it for evaluation rather than production. After the stack starts, `kortix self-host configure` sets your sandbox provider key, and you connect your own LLM key in the model picker. Self-hosted instances use your own key by default. The [self-hosting docs](https://kortix.com/docs) carry the full path.

## What the agent and trigger do

The `ops-agent` performs company operations work and returns a finished artifact as a file in the repo. The `morning-digest` trigger is a cron schedule that starts a session with no person present; the `task-webhook` trigger starts the same agent on a signed webhook. When the work is ready, the agent opens a change request, and you read it as a diff before anything merges. Session work reaches `main` through a change request, and merge is default-deny for agents.

Each session gets its own isolated sandbox and its own branch. The agent reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. You pick the model per agent, per session or per message: any model provider with your own keys, or the ChatGPT plan you already pay for.

## Open source Eigent alternatives

Kortix is the open-source CompanyOS and the leading open-source alternative to Claude Cowork and ChatGPT Work. The table compares it with the desktop Cowork app and with two other open-source projects you can host.

| Criterion | Kortix | Eigent | OpenWork | Claude Cowork |
| --- | --- | --- | --- | --- |
| Open source | Yes, full | Yes, Apache 2.0 | MIT core; org control plane source-available | No, closed |
| Where it runs | Your VPC, on-prem, or Kortix Cloud | Your desktop (macOS, Windows, Linux), or a managed cloud | Your desktop, with an optional hosted cloud computer | Anthropic's cloud; no self-host |
| Unit you own | A whole company: agents, memory and connectors in one git repo | A desktop workspace on one machine | A desktop app per member | A subscription seat |
| Models | Any provider, your own keys | Cloud APIs, enterprise gateways, or local inference | More than 50 providers through your keys or local models | Anthropic only |
| Governance | Per-resource permissions, approval gates, an audit trail | SSO and access control in Enterprise | An org control plane, Den | Set inside the product |

The competitor columns state what each project publishes on its own pages, checked October 2026. [Eigent](https://github.com/eigent-ai/eigent) documents its local-first desktop deployment, its CAMEL multi-agent framework and its Apache 2.0 license in its repository. [OpenWork](https://github.com/different-ai/openwork) runs agents on your own files, with a separate Den control plane for organizations. [Claude Cowork](https://claude.com/product/cowork) is a closed product that runs in Anthropic's cloud. Each covers a narrower lane than Kortix, which combines the whole-company repo, self-hosting, any model with your keys, and a change request on every piece of finished work.

## Docs

- [Deploy an open source Eigent alternative with Docker Compose](docs/deploy-with-docker-compose.md)
- [Kortix vs Eigent](docs/kortix-vs-eigent.md)
- [Open source Eigent alternative FAQ](docs/faq.md)

## Live pages

The campaign site expands on this repository with sourced comparisons and setup steps:

- [What the open-source Eigent answer is](https://eigentalternative.com/)
- [Open source Eigent alternatives](https://eigentalternative.com/eigent-alternatives)
- [Kortix vs Eigent](https://eigentalternative.com/kortix-vs-eigent)
- [What Eigent costs](https://eigentalternative.com/eigent-pricing)
- [Self-hosting walkthrough](https://eigentalternative.com/self-hosting-eigent-alternative)
- [Open source Eigent alternative FAQ](https://eigentalternative.com/faq)

## Get started

Self-host is free, and managed Kortix Cloud starts on a free plan with 500 credits a month; paid credits run at 100 per dollar, $50 for 5,000 a month, with unlimited members and no per-seat charge. Current numbers are on the [Kortix pricing page](https://kortix.com/pricing). Start from one job on one host, then grow. Try [Kortix](https://kortix.com), read the [Kortix docs](https://kortix.com/docs), or read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna).
