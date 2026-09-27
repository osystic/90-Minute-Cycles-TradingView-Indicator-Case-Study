# Technical Overview

## Runtime model

The indicator is an overlay that coordinates several stateful chart-object families:

- boxes for Session / M90 / M30 / M10 structures;
- boxes and optional midpoint lines for breakers;
- lines for cycle/session opens;
- lines and labels for HTF Opens, Intraday Opens and previous-period H/L.

## Time model

The implementation uses `America/New_York` as the authoritative timezone for the accepted session and calendar conventions.

This avoids accidental dependence on the exchange's default daily boundary where the project specification requires New York calendar boundaries.

## Cycle rendering

Each family maintains state for the active/latest range. A live-mode path updates the right edge using the current chart bar, preventing future scheduled geometry from appearing before those bars occur.

## Breaker tracking

For each applicable cycle family, the runtime tracks:

- current cycle key;
- high and low values;
- exact source timestamps / bar indices;
- source candle high/low geometry;
- completed-state marker;
- latest rendered high/low breaker objects.

The renderer projects the right edge using bar indices rather than timestamp arithmetic.

## Previous-period H/L

Session, Daily, Weekly, Monthly and Yearly ranges are tracked separately.

The displayed line begins at the exact high- or low-forming candle and extends right. High and low therefore remain independently anchored.

## Yearly refinement

The yearly path uses:

1. deeper 15-minute history to preserve reach;
2. candidate detection at that resolution;
3. nested 1-minute intrabar refinement for exact source-candle anchoring;
4. special handling of Jan-1 00:00 so the accepted year begins at 00:01.

## Display-size mapping

Public-facing options are:

- Small
- Medium
- Large

Small preserves the prior release's label appearance. Medium and Large increase readability while leaving level calculations untouched.

## Object management

Chart-object pools and latest-state replacement rules are used to limit uncontrolled stacking and stay within TradingView object limits.