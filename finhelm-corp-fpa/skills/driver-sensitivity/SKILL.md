---
name: driver-sensitivity
description: Rank which inputs actually move the forward number, so attention goes to the few that matter. Use when someone asks what drives the forecast, where to focus, which assumptions matter most, what to negotiate hardest, or when a plan has too many assumptions to manage.
---

# Driver sensitivity

Every plan rests on dozens of assumptions. A handful of them determine the outcome and the rest are rounding. Teams routinely spend their review time on the wrong ones, usually the assumptions that are easiest to argue about rather than the ones with leverage.

## Step 1. Inventory the assumptions honestly

List every input the forecast depends on, including the ones nobody wrote down. The unwritten assumptions are frequently the most consequential: an assumed collection period, an assumed close rate, an assumed start date for a hire.

For each, record the current value, who owns it, and where it came from. "Where it came from" separates a measured input from a negotiated one, and negotiated inputs deserve more scrutiny.

## Step 2. Establish a plausible range for each, not a guess

Sensitivity analysis is only as good as the ranges. A range invented for the exercise produces a ranking that is also invented.

Ground each range in something: historical variability of that input, an external benchmark, a contractual floor or ceiling, or the owner's genuine best and worst case. Where an input has history, use it. Where it does not, say the range is judgment and name whose.

## Step 3. Rank by impact, not by attention

Move each input across its plausible range, hold the others, and measure the effect on the outcome that matters. Rank by the size of that effect. Call the computation tool for the figures.

The output is usually uncomfortable and that is its value. The assumption the team argues about most is frequently not in the top five, and an input nobody has discussed often is.

## Step 4. Split the ranking by controllability

Impact alone does not tell you what to do. Cross it with control.

| | High impact | Low impact |
| --- | --- | --- |
| **Controllable** | Act here first. This is where management effort pays. | Delegate or ignore. |
| **Not controllable** | Monitor closely, build a contingency, hedge if possible. | Ignore. |

The top-left quadrant is the management agenda. The bottom-right is where review meetings usually go.

## Step 5. Present the few, not the many

Report the top three to five drivers and stop. A ranked list of twenty is a spreadsheet, not a recommendation.

For each: the input, its plausible range, the swing it causes, who owns it, and the one action that would narrow it. Narrowing a range is often more valuable than improving the central estimate, since it reduces the uncertainty everything downstream inherits.

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

Inventing ranges to make the analysis run. Ranking without splitting by controllability, which produces insight nobody can act on. Reporting every driver instead of the few that matter. Treating a sensitivity table as the deliverable rather than the recommendation it supports. Running sensitivity on a baseline whose reliability was never checked.
