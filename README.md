# 90 Minute Cycles TradingView Indicator - Engineering Case Study

> **OSYSTIC ENGINEERING CASE STUDY · PUBLIC SHOWCASE · SANITIZED · PORTFOLIO-SAFE**
>
> This repository contains **no client identity, no confidential Pine Script source, no private screenshots, no private conversations, no payment information, no credentials, and no proprietary delivery package**.\n\n![Architecture](assets/architecture.svg)

## Company showcase classification

| Attribute | Public classification |
|---|---|
| Publisher | **OSYSTIC** |
| Artifact type | Engineering case study / capability proof |
| Platform | TradingView |
| Language | Pine Script v6 |
| Engagement | Completed custom indicator engineering project |
| Publication model | Sanitized public showcase with independent Git history |
| Confidential implementation | Excluded and retained privately |
| Profitability claim | None |
| Intended use | Portfolio, proposals, technical due diligence, capability review |

## What this repository is

An anonymized engineering case study for a custom multi-timeframe TradingView overlay built around session structure, 90-minute cycles, lower-timeframe cycle decomposition, breaker visualization, market-open references, and source-anchored previous-period H/L levels.

The engagement was highly iterative and reference-driven. The engineering work focused not only on calculations, but also on exact chart behavior: active boxes had to grow progressively, breaker zones had to use the correct source candle and projection semantics, labels had to remain readable without collisions, and higher-timeframe H/L levels had to obey explicit New York calendar conventions rather than exchange-session defaults.

## Outcome

The project was completed and client accepted.

Final delivery included:

- Session, M90, M30 and M10 visual structures.
- Progressive live-cycle rendering.
- Reference-aligned Session / M90 label hierarchy.
- Breaker zones with exact chart-bar extension.
- Optional breaker midpoint lines.
- Higher-timeframe and intraday open references.
- Previous Session / Daily / Weekly / Monthly / Yearly H/L levels.
- Exact source-candle anchoring for the displayed H/L levels.
- New York calendar period logic.
- Configurable Small / Medium / Large labels for HTF Opens, Intraday Opens and H/L levels.
- Regression checks across MNQ, NQ and ES chart contexts.

## Public vs. private repository boundary

| Area | This public showcase | Confidential engineering repository |
|---|---|---|
| Visibility | **Public** | **Private** |
| Purpose | Portfolio / capability proof | Engineering source of truth |
| Pine Script implementation | **Not included** | Retained privately |
| Client identity | **Not included** | Protected |
| Private screenshots / conversations | **Not included** | Controlled |
| Commercial / payment information | **Not included** | Controlled |
| QA methodology summary | Included | Full delivery context retained |
| Safe to share publicly | **Yes** | **No** |

This repository is not a fork, mirror, or source-code export. It has independent sanitized history.

## Engineering architecture

```text
New York session/time model
           |
           v
Session windows and cycle schedule
           |
           +--> Session outer structures
           +--> M90 cycles
           +--> M30 cycles
           +--> M10 cycles
           |
           v
Source-candle H/L tracking
           |
           +--> Breaker zones
           +--> Previous Session H/L
           +--> Previous D/W/M/Y H/L
           |
           v
HTF / intraday open references
           |
           v
Display state + progressive live rendering
           |
           v
Label hierarchy / size / disclosure-safe presentation
```

## Engineering highlights

- **Progressive active geometry:** current cycle boxes grow only through the live candle instead of rendering their entire scheduled future span immediately.
- **Source-candle anchoring:** breaker and H/L structures begin at the candle that actually formed the relevant high or low.
- **Chart-bar breaker semantics:** an extension value of 10 projects exactly ten chart candles ahead.
- **Controlled breaker history:** the display avoids endless historical stacking.
- **Timeframe-aware behavior:** the smallest breaker family is restricted to the intended ultra-low timeframe context.
- **New York calendar rules:** D/W/M/Y levels follow explicit calendar boundaries instead of inheriting CME-style 18:00 period boundaries.
- **Yearly precision:** long-history discovery is combined with targeted 1-minute refinement for exact yearly extreme anchoring.
- **Boundary handling:** Jan-1 00:00 is deliberately excluded from the accepted yearly period so the year starts at 00:01 New York time.
- **Visual hierarchy:** parent Session labels and M90 labels use independent vertical tiers to prevent LO/LO2, AM/AM2 and PM/PM2 collisions.
- **Accessible settings:** final polish added three independent label-size dropdowns while preserving the previous appearance at the Small setting.

## Technology

`TradingView` · `Pine Script v6` · `multi-timeframe chart logic` · `New York timezone handling` · `stateful boxes/lines/labels` · `request.security` · `lower-timeframe intrabars` · `bar replay QA`

## What is intentionally not claimed

This showcase does **not** claim:

- profitability, alpha, win rate, ROI, or loss prevention;
- that the indicator is a trading strategy or automated execution system;
- that public documentation reproduces the confidential implementation;
- identical behavior on every symbol, data feed, chart type, or TradingView account tier;
- redistribution rights for the confidential Pine source;
- that visual similarity to a reference implies source-code equivalence.

## Read more

- [Full case study](case-study.md)
- [Technical overview](docs/technical-overview.md)
- [Validation evidence](docs/validation-evidence.md)
- [Engineering lessons](docs/lessons-learned.md)
- [Disclosure boundary](docs/disclosure-boundary.md)
- [Publication and reuse notice](NOTICE.md)
- [Security policy](SECURITY.md)

## Disclosure boundary

Only sanitized architecture, requirements patterns, validation methodology, public-safe outcomes and engineering lessons are published here. Confidential Pine source, client identity, private screenshots, conversations, commercial records and delivery artifacts are intentionally excluded.

**OSYSTIC** · Engineering systems, automation, AI and trading technology.

## OSYSTIC PACE evidence framework

- **P - Problem and constraints:** reproduce a complex reference-driven chart workflow without access to proprietary source while preserving exact time, anchor, projection and visual semantics.
- **A - Architecture and decisions:** New York time model, stateful multi-timeframe cycle engine, source-candle H/L tracking, bar-index breaker projection, hybrid yearly-history refinement and bounded chart-object lifecycle.
- **C - Contribution and delivery:** OSYSTIC engineered, iteratively refined, tested and delivered the Pine Script v6 indicator through acceptance-driven QA.
- **E - Evidence and outcomes:** compile/add-to-chart success, focused behavioral gates, MNQ/NQ/ES regression checks, final label-readability verification and client acceptance.

## Governance and publication

This repository follows the OSYSTIC sanitized public-showcase model.

- Private engineering source remains separate.
- Public history is independently sanitized.
- Publication boundary: [docs/publication-record.md](docs/publication-record.md)
- Ownership/reuse: [OWNERSHIP.md](OWNERSHIP.md)
- Security/disclosure: [SECURITY.md](SECURITY.md)
- Maintenance/withdrawal runbook: [docs/runbook.md](docs/runbook.md)
