---
name: board-package
description: Build a board-ready financial narrative that presents a range without losing the room. Use when preparing board materials, a quarterly business review, an investor update, or a lender package, and especially when the underlying analysis is probabilistic and has to be made legible to a non-finance audience.
---

# Board package

A board package has a harder job than it appears. It must be honest about uncertainty and still be decisive, in front of an audience that is intelligent, time-constrained, mostly non-finance, and conditioned to expect single numbers.

Presented badly, a range reads as evasion. Presented well, it reads as the most credible thing in the room.

## Step 1. Decide what the board actually needs to decide

Start from the decisions on the agenda and work backward. A board package is not a status report with charts; it is the material required for a specific set of decisions.

If nothing requires a decision, the financial section should be short. Length signals importance, and using length on a quarter that needs no action trains the board to skim the quarter that does.

## Step 2. Open with the reading, not the data

The first slide states where things stand and what needs deciding. Everything after it is support.

> "We are inside the plan envelope for the quarter. Cash runway is fourteen months central, eleven in the downside. One decision today: whether to hold the two open engineering roles until the enterprise deal resolves."

## Step 3. Present the range so it lands as confidence

Order matters. Central case first, so there is something to hold onto. Then the range. Then, immediately, what drives the spread.

> "Fourteen months. Realistically between eleven and eighteen. Almost all of that spread is collection timing on two accounts, which is why we are focused on those two collections rather than on cutting spend."

Never present a range without its cause. The cause is what converts a range from hedging into analysis. And never retreat to a single number when asked; give the central case again with its range attached, every time, and the room adjusts within two meetings.

Every figure in the package, the central case, the range and the reliability band, comes from the computation tool's result and its receipt. Do not derive a range or a band inline from ledger rows the ERP connector returned, and do not estimate one. If the tool is unavailable, build the narrative structure and mark each figure as requiring the connector.

## Step 4. Introduce reliability as evidence, not jargon

If forecast reliability has been scored, use it as the reason to believe the rest of the package, and explain it in one plain sentence. Never present the composite bare.

> "Our forecasting has been running in the second band, which means the plan has been reliable enough to build on, with a modest optimistic bias in operating expense that we have adjusted for here."

Explain that lower is better, once, every time. Do not assume prior familiarity.

## Step 5. Show scenarios as paths with triggers

Do not present three columns of numbers. Present three stories with the signal that indicates each one is happening and the lead time it provides. That is what lets a board govern rather than react.

## Step 6. End on decisions with recommendations

Every decision item carries a recommendation. A board that is asked to choose without one is being asked to do management's work, and the discussion drifts.

State the recommendation, the reasoning, and what would change it.

## Style discipline

Numbers in tables, not in prose. Every figure traceable to the ledger. No adjectives doing analytical work: "strong quarter" means nothing, "revenue landed at the top of the plan range" means something. No surprises in the room that a director should have heard by phone first. Consistent format quarter to quarter, since a board reads a package it recognizes far faster than one it has to relearn.

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

Leading with data instead of the reading. Presenting a range without its driver. Retreating to a single number under pressure. Using scoring language without explaining it. Scenario tables with no triggers. Decision items with no recommendation. Making the package longer in a quarter that needed nothing. Quoting a range or a band that no computation receipt supports.
