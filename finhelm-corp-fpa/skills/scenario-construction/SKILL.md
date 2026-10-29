---
name: scenario-construction
description: Build defensible base, upside, and downside cases that a board will accept. Use when someone asks for scenarios, a downside case, what-if analysis, a bear case, contingency planning, or when preparing a plan that has to survive scrutiny from a board, lender, or investor.
---

# Scenario construction

Three cases labeled base, upside, and downside are standard practice and usually meaningless, because they are typically the same plan with revenue multiplied by three different numbers. That construction survives no scrutiny: it says the future is uncertain without saying anything about how.

A defensible scenario changes assumptions, not outputs.

## Step 1. Start from drivers, never from the total

If the downside was produced by taking the base case and reducing revenue fifteen percent, it is not a scenario. Nothing in the business would produce a uniform fifteen percent reduction across every line.

Build each case from the driver level: what close rate, what collection period, what hiring pace, what unit cost. Then let the totals fall out. The totals are the *result* of the scenario, not its definition.

## Step 2. Give each case a story a person could tell

Every scenario should be describable in one sentence about the world, without reference to any number.

- Base: "Sales continues at its trailing-six-month pace, the two open roles are filled by the end of the quarter, and collections hold at current terms."
- Downside: "The enterprise deal slips two quarters, collections stretch by fifteen days, and we hold hiring."
- Upside: "The enterprise deal closes this quarter and the channel partnership produces its first three deals."

If a case cannot be told as a story, it is arithmetic wearing a label. The story is also what lets someone recognize the scenario when it starts happening.

## Step 3. Move only the drivers the story moves

Discipline here is what makes the cases credible. If the downside story is a deal slipping, then the deal slips and the associated commission does not pay, but rent does not change. Uniformly worsening every line signals that no thinking took place.

## Step 4. Make the downside genuinely uncomfortable

Most downside cases are mild, because they are drafted by people who want the plan approved. A downside that everyone finds tolerable provides no information and no protection.

The useful test: the downside should be the case that forces a decision. If nothing would have to change, it is not a downside, it is a slightly worse base.

## Step 5. Attach triggers and lead time

A scenario without a trigger is a document. For each case, state the observable signal that indicates it is happening, and how much warning that signal provides before action is required.

> "If two of the three deals in late-stage do not close by the fifteenth, we are on the downside path. That gives roughly six weeks before the hiring decision has to change."

This converts scenario planning from an exercise into an operating instrument.

## Step 6. Place the cases against the distribution

Three cases are three points. If a distributional forecast is available, place them against it, so everyone can see whether the downside is genuinely a downside or merely the middle of the range with a pessimistic name. Call the computation tool for those figures rather than asserting where the cases sit.

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

Scaling a total instead of moving drivers. Cases with no story. Moving every line in the same direction. A downside nobody would act on. No triggers, so the work is never used again. Presenting three cases as if they bound the possibilities, when they are three samples from a much wider range.
