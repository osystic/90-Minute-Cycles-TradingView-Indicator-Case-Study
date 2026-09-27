# Full Case Study

## 1. Engagement context

OSYSTIC was asked to engineer a custom TradingView overlay that reproduced a reference-driven market-structure workflow without access to the original proprietary source.

The practical challenge was broader than drawing time boxes. The delivered indicator had to coordinate several visual layers, preserve exact period semantics, and remain stable under live chart progression and Bar Replay.

## 2. Core problem

The required overlay combined:

- parent trading sessions;
- 90-minute cycle structures;
- nested 30-minute and 10-minute structures;
- breaker zones derived from completed ranges;
- session / cycle opening references;
- higher-timeframe and intraday opens;
- previous-period high / low levels;
- a strict visual hierarchy so labels and boxes remained readable.

Small implementation details materially affected correctness. For example, an active box pre-drawn across its full future schedule looked wrong even when its timestamps were mathematically correct. Likewise, a breaker that extended ten minutes instead of ten chart bars did not match the required chart behavior.

## 3. Key engineering decisions

### Progressive live rendering

Active Session/M90/M30/M10 boxes were changed to grow with the current chart candle. Completed structures remain historical; the live structure reflects only information available up to the present bar.

### Breaker source and projection

Breaker zones use the actual chart candle that formed the high or low as their left boundary. Their right boundary is projected using chart-bar indices, so an extension of 10 always means ten candles on the current chart.

### Bounded breaker display

Historical breakers do not accumulate indefinitely. The implementation tracks the current/latest completed structures by family to preserve chart readability and object limits.

### Explicit New York period model

Previous D/W/M/Y H/L levels use New York calendar periods instead of exchange-session boundaries.

The accepted conventions were:

- previous day: 00:01-23:59 New York;
- previous week: Monday 00:01-Friday 23:59 New York;
- previous month: calendar month;
- previous year: calendar year beginning 00:01 on Jan 1.

### Yearly-history precision

A yearly level creates a special TradingView challenge: exact 1-minute anchoring can require more history than is practical to request entirely at 1-minute resolution.

The solution used a deeper 15-minute historical scan to find candidate yearly extreme bars, then refined candidate bars using nested 1-minute intrabars. This preserved long reach while anchoring the final yearly H/L line to the exact 1-minute source candle.

### Label hierarchy

Parent Session labels and M90 labels can share similar horizontal positions. Fixed vertical tiers were therefore introduced so the parent session label remains visually above the lower cycle label.

### Readability without logic changes

The final client-requested refinement added Small / Medium / Large label-size controls for three display families. The Small option deliberately maps to the previous production appearance so the feature is backward-compatible visually.

## 4. QA approach

The project used focused gates instead of relying on a single final screenshot.

Validation covered:

- compile / add-to-chart;
- session and cycle visual hierarchy;
- progressive active-box right edges;
- exact +10 breaker projection;
- optional breaker midpoint;
- Session/Daily/Weekly/Monthly/Yearly H/L;
- exact yearly source anchoring;
- Jan-1 00:00 exclusion;
- MNQ / NQ / ES visual regression;
- final Small/Medium/Large label rendering.

See [Validation evidence](docs/validation-evidence.md).

## 5. Delivery outcome

The final release was accepted by the client. The last enhancement was an isolated readability feature rather than a logic rewrite, which allowed the project to close without reopening previously approved cycle, breaker or H/L behavior.

## 6. Engineering value demonstrated

This engagement demonstrates OSYSTIC capability in:

- Pine Script state management;
- multi-timeframe time-series engineering;
- chart-object lifecycle control;
- reference-driven UI reproduction;
- timezone-sensitive market logic;
- lower-timeframe data refinement;
- regression-focused QA;
- iterative client acceptance workflows.

## 7. Public disclosure note

This case study intentionally explains architecture and engineering decisions without publishing the proprietary Pine implementation or private client material.