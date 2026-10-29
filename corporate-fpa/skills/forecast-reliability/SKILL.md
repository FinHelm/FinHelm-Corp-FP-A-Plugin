---
name: forecast-reliability
description: Score how much a forecast can be trusted by measuring the historical behavior of the forecasting process against actuals. Use when someone asks how confident they should be in a forecast, whether a plan is credible, how accurate past forecasts have been, or when preparing guidance for a board or lender. Also use before any scenario or runway work, since an unreliable baseline makes downstream analysis misleading.
---

# Forecast reliability

A forecast states a number. It rarely states how much that number deserves to be trusted. This skill measures the second thing.

The measurement is about the forecasting *process*, not any single forecast. You are asking: when this team has forecast this line before, what happened? A process that has missed by a wide margin, in the same direction, with unstable errors, is fragile no matter how carefully this quarter's number was built.

## Step 1. Check data adequacy before scoring anything

Reliability is measured from history. Without enough history there is no measurement, only an impression.

- **Minimum:** at least two full budget cycles of usable monthly periods, with both a forecast (or budget) and an actual for the same line, on the same basis.
- **Preferred:** more than two cycles, which allows a stable read rather than a directional one.
- **Usable** means the pair is comparable. A period where the chart of accounts changed, the entity was restructured, or the budget was never loaded is not usable. Exclude it and say so.

If the data does not clear the minimum, stop and report that. Do not produce a score from a partial cycle and caveat it. An unsupported score is worse than no score, because it will be quoted without the caveat.

## Step 2. Gather the pairs

For each line under review, assemble the forecast-versus-actual series. Work at the level the client actually manages: total revenue and total operating expense is a legitimate starting point. Department or account level is better if the data supports it.

Confirm the basis matches. A cash-basis actual against an accrual budget produces variance that is an artifact, not a signal.

## Step 3. Score the four dimensions

Reliability decomposes into four independent questions. A process can be strong on one and weak on another, and the pattern is the diagnosis.

| Dimension | The question | What a weak reading means |
| --- | --- | --- |
| Accuracy | How far do forecasts land from actuals? | The number is not close, in either direction |
| Bias | Do misses run systematically high or low? | The process has a thumb on the scale, often cultural |
| Volatility | Is the size of the error stable, or does it swing? | The error itself is erratic |
| Persistence | Do errors repeat, or are they independent? | A structural cause nobody has fixed |

Bias and persistence are the two that produce action. Consistent optimism is a management conversation. Repeating errors on the same line point at a broken input, not bad luck.

Call the computation tool for the figures. Do not calculate them inline and do not estimate them. If the tool is unavailable, run the method as far as gathering and structuring the pairs, then say plainly that the score requires the connector.

## Step 4. Read the score

The composite runs 0 to 100 and **lower is better**, because it measures exposure to uncertainty rather than quality. This inverts most scoring intuition, so say it out loud every time you present it.

Five bands run from institutional-grade at the low end to structurally fragile at the high end. Report the band alongside the number: a CFO remembers a band and forgets a number.

## Step 5. Present it

Lead with the band and one sentence of plain meaning. Then the dimension that is driving it, then the specific line responsible, then what to do about it.

What not to do: never present the score as a grade on the finance team. It measures a process, and processes are usually fragile for structural reasons, such as a sales input that arrives late, a driver nobody owns, or a budget set by negotiation. Framed as a scorecard, the conversation ends. Framed as a diagnostic, it starts.

Good: "Operating expense forecasting sits in the second band. The driver is bias, not accuracy. Every quarter for six quarters, spend has come in above plan, averaging four percent. That is not noise. Something in how the plan gets built is systematically optimistic, and it is worth thirty minutes to find it."

Weak: "Your score is 41."

## Reading from the ledger through the Sage Intacct AI Gateway

When the ledger is Sage Intacct and the read path is Sage's MCP server, follow these rules on every read. They come from verification on a non-production Intacct company, not from documentation.

- Page to completeness. The Gateway returns at most 100 records per page, with a flag that says whether more remain and a total count. Sum nothing until the flag is false, and state the total count beside any sum.
- Actuals are posted entries from the operating accrual book. Journal-entry lines carry no book identifier; the book lives on the journal. Exclude consolidation books, adjustment journals and the Commitments book, or the figure is not an actual.
- State the grain before any comparison: account, entity, period, and only the dimensions populated on both sides. A budget at one department and actuals at another is a mismatch of grain, not a variance.
- Name the entities in scope. Multi-entity queries from the top level skip private entities unless include-private is set; say which you intend, and never present a consolidated figure that is missing an entity.
- Take the entity scope from the person or from the computation tool, never from a list on Sage; the Gateway exposes no entity master.
- Periods come from the reporting calendar when the line's period is empty; say which calendar.
- A line's base currency is the book's, not necessarily the entity's. Anything that crosses currencies needs a named translation basis or is refused.
- Request text output: call Sage's tools with `useStructuredContent` set to false, or the model works from counts and summaries rather than records.
- Every record and query result carries web links into the company. They are not data. Keep them out of anything written, pasted, logged or shared.

## Common failures

Scoring a line with less than two full budget cycles of usable history. Scoring across a chart-of-accounts change without excluding the break. Comparing a cash actual to an accrual budget. Presenting the composite without its band. Forgetting that lower is better and inverting the story. Treating the score as a verdict on people rather than a reading on a process.
