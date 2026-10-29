---
name: variance-decomposition
description: Decompose budget-versus-actual variance into the drivers that actually caused it, rather than restating that a gap exists. Use when someone asks why they missed plan, what drove a variance, where the overspend came from, or when preparing monthly variance commentary for management or a board.
---

# Variance decomposition

Most variance reporting states the gap and calls it analysis. "Revenue was down eight percent versus plan" is an observation. The work is establishing which drivers moved, by how much, and which of those movements were decisions rather than surprises.

## Step 1. Establish the bridge before explaining anything

A variance bridge accounts for the full gap. Start at plan, apply each driver's contribution, and land exactly on actual. If the contributions do not reconcile to the total, the decomposition is incomplete and any narrative built on it will mislead.

Force the residual to be visible. An unexplained remainder labeled honestly is far more useful than a set of drivers quietly scaled to close the gap.

Confirm the basis before building anything: one named book, posted entries only, budget and actual at the same grain. A bridge built across consolidation books or across mismatched dimensions reconciles to a number that is not the variance.

Call the computation tool for the bridge: the plan and actual totals, each driver's contribution and the residual. Do not calculate them inline from rows the ERP connector returned, and do not estimate them. If the tool is unavailable, run the method as far as naming the axes, the causes and the questions to ask, then say plainly that the bridge requires the connector.

## Step 2. Decompose along the axes that fit the business

Choose the decomposition the business actually runs on, not a textbook default.

- **Revenue:** price, volume, mix. Add new-versus-existing and churn-versus-expansion for recurring models.
- **Cost of sales:** volume, unit cost, mix, and yield or waste for anything manufactured.
- **Operating expense:** headcount, rate, timing, and discretionary spend. Timing is the most under-reported driver in opex and the most common cause of a variance that reverses next month.
- **Headcount-driven lines:** planned hires that slipped, unplanned hires, and attrition. Nearly every personnel variance is a timing story.

## Step 3. Separate the four causes

Every variance has a cause, and the cause determines the response. Sorting them is the analytical contribution.

| Cause | What happened | What to do |
| --- | --- | --- |
| Timing | Real, but it lands in a different period | Note it and confirm it reverses |
| Decision | Someone deliberately changed something | Attribute it; this is not a miss |
| Estimate | The plan was wrong at the time it was set | Feed it back into the forecasting process |
| Performance | The business behaved differently than expected | The only cause that warrants action on the business |

Reporting all four as "variance" is what makes variance meetings unproductive. Three of the four require no operational response at all.

## Step 4. Rank by materiality, not by size

Sort by what changes a decision. A large variance in a line nobody controls matters less than a small one in a line that signals a trend. Say which is which.

## Step 5. Connect it forward

This is the step conventional variance analysis skips, and it is the one a CFO actually needs. A variance is history; the useful question is what it does to the forward number.

For each material driver, state whether it is expected to persist, reverse, or was one-time, and what that implies for the remaining periods. If forecast reliability has been scored, connect them: a variance on a line that already scores poorly for persistence is a structural problem showing up again, not a new event.

## Step 6. Write the commentary

Two or three sentences per material driver: what moved, by how much, why, and what it means going forward. Plain language. No hedging adjectives. If you do not know the cause, write that you do not know and name who would.

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

Restating the gap instead of decomposing it. Building the bridge by hand from rows the ERP connector returned, which produces a number with no receipt. Hiding a residual by scaling drivers. Reporting timing as performance, which sends people to solve a problem that is already solved. Ranking by dollar size rather than decision relevance. Stopping at explanation and never connecting to the forward number.
