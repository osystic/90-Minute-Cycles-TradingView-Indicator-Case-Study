# Engineering Lessons

## 1. Visual correctness is behavioral correctness

A time box can use mathematically valid boundaries and still fail the user experience if it renders future geometry before the chart reaches those bars.

## 2. "Extend 10" needs an explicit unit

Timestamp projection and chart-bar projection are not interchangeable. The accepted meaning was ten chart candles, so bar-index coordinates were the correct abstraction.

## 3. Source anchoring matters

Market-structure levels are easier to audit when the line or zone begins at the candle that actually formed the extreme instead of an arbitrary period boundary.

## 4. Exchange periods and calendar periods are different requirements

Trading platforms often expose exchange-session conventions. A project that explicitly asks for New York calendar periods needs its own period model.

## 5. Long history and exact precision may need a hybrid data strategy

Scanning an entire year at 1-minute resolution is not always the right engineering tradeoff. Coarse historical discovery plus fine intrabar refinement can provide both reach and precision.

## 6. Parent/child visual layers need deliberate hierarchy

When Session and sub-cycle labels share x positions, fixed independent vertical tiers are more reliable than hoping auto-layout will avoid collisions.

## 7. Late-stage feature requests should be isolated

The final label-size enhancement was implemented through the label renderer only. Keeping it isolated protected already-approved H/L calculations, cycle timing and breaker behavior.