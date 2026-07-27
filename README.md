# Ever Cifuentes

Backend and platform engineer in Bogotá, Colombia. Go and TypeScript, and a
particular interest in the parts that decide whether software survives contact with
real users: contracts between services, quotas that reconcile, failure paths that
were designed rather than discovered, and release gates that are allowed to say no.

I write about that at **[bitkode.dev](https://bitkode.dev)** — a publication I also
designed and built, and the last entry below.

---

## Selected work

Four projects, each demonstrating something different. All of them are inspectable
past the source code — specifications, architecture decisions, and delivery records
are in the repositories too.

### [hlab](https://github.com/aikssen/hlab) · Go

A CLI and full-screen TUI that creates and manages Proxmox VMs and LXC containers.
You think *"I want a new server"*, not *"I want to configure Terraform"*.

It discovers the cluster through the Proxmox API, asks only what it cannot infer,
and then **orchestrates the official tools** — Terraform for the guest lifecycle,
Ansible for provisioning — rather than reimplementing them, so your infrastructure
stays in a format that outlives my tool.

`brew install aikssen/tap/hlab` · Apache-2.0 · shipping since v0.1.0

### [glazz-chat](https://github.com/aikssen/glazz-chat) · Go + Next.js

An LLM chat product. The chat is not the interesting part — wiring a model into an
application takes an afternoon.

What took the work: ordered realtime streaming with a bounded replay window so a
reconnect can catch up, quota reserved before a generation and settled against real
usage afterwards, an internal provider gateway so the vendor stays replaceable,
model discovery kept separate from model exposure, and prompt content that never
enters logs, traces, metrics, or the audit trail.

It was specified before it was written. The original prompt, the 61-question
requirements round that followed, the decisions where I overrode the proposal, and
the reasoning behind them are all in `docs/`.

### [llm-benchmark-for-dev](https://github.com/aikssen/llm-benchmark-for-dev) · Go

Seventeen models, one Go backend assessment, scored against a 280-point rubric
across twelve categories.

Every submission was built and run for real, including `go test -race`, with
targeted probes added where the submitted tests avoided the dangerous path. The
useful finding was not the leaderboard: documentation quality was uniformly high
and engineering correctness was not, and concurrency separated the two.

Full rubric, every submission, and a report per model.

### notifications system · TypeScript

An event-driven notification pipeline, split across three repositories:

- **[notifications-dispatch-service](https://github.com/aikssen/notifications-dispatch-service)** — a background worker that consumes Kafka events, persists them for idempotency and auditability, and delivers to client-defined webhooks under subscription rules.
- **[notifications-subscription-service](https://github.com/aikssen/notifications-subscription-service)** — resolves subscriptions and simulates webhook success and failure, so the whole flow runs end to end locally.
- **[notifications-self-service](https://github.com/aikssen/notifications-self-service)** — the self-service surface over it.

### [bitkode.dev](https://bitkode.dev) · Astro + Cloudflare

An engineering publication I designed and ship, not a hosted blog.

Astro rendered at the edge on Cloudflare Workers, four content collections, and every
piece published as paired English and Spanish versions rather than machine
translations. Client-side search through Pagefind, RSS and sitemap, and a design
system where each engineering domain carries its own colour tint across light and
dark themes.

The diagrams are components, not screenshots — one bespoke Astro component per
concept, so an explanation gets corrected in a pull request instead of redrawn.

Its editorial standard is written down as well: article template, writing guide,
cover art direction. Same reason the code has specifications.

---

## How I work

**Specify before writing.** Not documentation produced afterwards for someone else —
the decisions written down before there is code to defend them with. The questions I
cannot answer yet are the design I was about to skip.

**Let machines enforce boundaries.** API contracts generate both sides and CI fails
when the generated output drifts. A boundary a reviewer might notice is weaker than
one the build refuses to cross.

**Verify in proportion to risk.** Unit tests where logic lives, integration tests
against real PostgreSQL and Redis, the race detector and goroutine-leak checks
around anything concurrent, browser tests for the paths users actually take. The
most common defect in fast-written code is an assertion nobody checked.

**Say where things stand.** Glazz has passing pipelines, five tagged releases, and a
README that states it is not approved for public production traffic — because the
production milestone is open. If a repository of mine claims something is ready, I
would like that claim to be worth something.

---

📍 Bogotá, Colombia · 🌐 [evercifuentes.com](https://evercifuentes.com) ·
✍️ [bitkode.dev](https://bitkode.dev) · 🧰 [hlab.sh](https://hlab.sh)
