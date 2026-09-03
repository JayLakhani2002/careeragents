# careeragents

**A multi-agent job search pipeline that runs in your terminal.**

Companies use AI to filter candidates. This gives candidates AI to filter companies.

Paste a job URL. An agent scores it against your actual CV across the A–H report structure,
writes an evaluation report, generates a CV tailored to that posting, and files it in
a tracker — so you spend your time on the five roles worth applying to instead of
the fifty that were never going to work out.

```
you: https://company.com/careers/ai-engineer-berlin

  → verifying posting is live
  → evaluating (A–H): fit, comp, location, culture, growth, risk, legitimacy, answers
  → 4.2/5 — strong archetype match, comp above floor, hybrid Berlin
  → tailored CV written to output/
  → tracked as #001

  Report: reports/001-company-2026-09-03.md
```

---

## What it does

| | |
|---|---|
| **Evaluate** | Score any posting A–H against your profile. Reports include a legitimacy check for scam and ghost-job signals. |
| **Scan** | Sweep 137 company job boards (Greenhouse/Ashby/Lever APIs) with **zero LLM cost**. |
| **Tailor** | Generate a CV per posting — HTML or LaTeX → PDF. Keywords get reformulated, never fabricated. |
| **Track** | Every application in a markdown table with canonical states and an append-only status ledger. |
| **Prep** | Company research, STAR story matching, mock interviews, red-flag analysis. |
| **Follow up** | Cadence calculator that tells you who to chase and when. |
| **Analyze** | Rejection patterns, funnel velocity vs market benchmarks, skill gaps across your pipeline. |

Runs on any CLI implementing the [open agent skill standard](https://agentskills.io) —
Claude Code, Codex, Cursor, OpenCode, Copilot, Qwen, Kimi, Antigravity, Grok.

## Quick start

```bash
git clone https://github.com/JayLakhani2002/careeragents.git
cd careeragents
npm install
```

Then open your CLI in the folder and say **"set me up"**. It will ask for your CV and
a few targeting details, then write `cv.md`, `config/profile.yml`, `portals.yml` and
your tracker. Takes about two minutes.

After that, just talk to it:

```
"evaluate this: <url>"       "scan for new roles"
"where does everything stand" "prep me for the Datadog interview"
"generate a CV for Zalando"   "what skills am I missing"
```

### Running on Codex

Codex doesn't guarantee slash-command support, so drive it with plain language
instead. Interactive: run `codex` in the repo root and ask it to run a mode
("run the scan mode", "evaluate this JD: <url>"). Headless: `codex exec "prompt"`
for one-shot workers. See [CODEX.md](CODEX.md) and [docs/SETUP.md](docs/SETUP.md).

## Guarantees

| | |
|---|---|
| **Human in the loop** <!-- hitl: absolute guarantee. Do not add "usually", "generally", "normally", "typically", "by default", "unless", "without your permission", "automatically", or "by itself". The tool never submits an application. This is an absolute prohibition, not a default setting a user can flip. Translators: keep the row absolute. --> | The tool **never submits an application**. It fills forms, drafts emails and builds PDFs, then stops before Send. You make every final call. |
| **No fabrication** | Content is generated strictly from your own files. Keywords get reformulated, never invented. |
| **Postings are data** | Text scraped from a job posting cannot issue instructions, change rules, or trigger writes. |
| **Your data is local** | `cv.md`, profile, tracker and reports are gitignored and never leave your machine. |

## Design principles

Each guarantee above is enforced in the mode instructions, not left to the model's
discretion. The no-fabrication rule in particular means an unsupported claim is omitted
from your CV rather than invented to fill a gap.

## Docs

[Setup](docs/SETUP.md) · [Customization](docs/CUSTOMIZATION.md) · [Architecture](ARCHITECTURE.md) · [Scripts](docs/SCRIPTS.md) · [Automation](docs/AUTOMATION.md) · [FAQ](docs/FAQ.md) · [Running on a budget](docs/RUNNING_ON_A_BUDGET.md)

## Credit

**careeragents is a fork of [career-ops](https://github.com/career-ops-hq/career-ops)**,
created by [Santiago Fernández de Valderrama](https://santifer.io) ([@santifer](https://github.com/santifer)).

The evaluation framework, scoring architecture, mode system, and the overwhelming
majority of this codebase are his work, released under MIT. This fork adapts it and
takes it in its own direction; it is not affiliated with or endorsed by the upstream
project. If you find this useful, the credit belongs upstream — go star
[career-ops](https://github.com/career-ops-hq/career-ops).

Fork maintained by [Jay Lakhani](https://github.com/JayLakhani2002).

## License

MIT — see [LICENSE](LICENSE) and [NOTICE](NOTICE).
Original work © 2026 Santiago Fernández de Valderrama. Modifications © 2026 Jay Lakhani.
