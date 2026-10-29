---
name: cash-runway
description: Estimate cash runway as a range with confidence bands rather than a single date. Use when someone asks how long their cash lasts, when they run out, whether they can afford a hire or an investment, or when preparing runway figures for a board, a lender, or a fundraise.
---

# Cash runway

Runway is usually stated as one date, produced by dividing cash by an average burn. That date is presented with a confidence nobody actually has, and it is the number companies most often act on.

A range is both more honest and more useful, because the decisions runway drives are decisions about risk.

## Step 1. Establish the starting position

Confirm opening cash against the ledger, not a spreadsheet. Note anything that makes the number less liquid than it appears: restricted cash, a facility with covenants, receivables concentrated in one payer, a large payable about to clear.

## Step 2. Build burn from drivers, not from an average

An average of trailing burn embeds whatever was unusual in those months. Build forward instead from the components: payroll and the hiring plan, recurring vendor commitments, discretionary spend, and the collection pattern on receivables.

Separate committed from discretionary. The distinction is the entire basis of the management conversation later, since committed spend sets the floor and discretionary spend is the lever.

## Step 3. Let the uncertain inputs be uncertain

The reason a single-date runway misleads is that it forces a point estimate onto inputs that are genuinely variable. Collections slip. A large deal closes or does not. Hiring runs behind plan more often than ahead.

Identify which inputs carry real variability and let them vary. The result is a distribution of outcomes rather than one path. Call the computation tool for the figures; do not construct the distribution by hand and do not estimate the bands.

## Step 4. Report the band, not the point

Report the range with its confidence interval and the central case together. A useful framing:

> "The central case is fourteen months. The realistic downside is eleven, the upside is eighteen. The spread is driven almost entirely by collection timing on two accounts."

The final clause is the valuable one. A range without its cause is just a wider number. A range with its cause is a to-do list.

## Step 5. Make it decision-ready

Runway matters because of the decisions attached to it. State them.

- **The trigger:** at what cash balance or date does a decision become forced?
- **The lever:** which discretionary spend most extends the downside case?
- **The dependency:** which single input most narrows the range if it resolves?

## Step 6. Handle the board conversation

Boards are used to one number and some will ask for one. Do not retreat to a single date. Give the central case first, then the range immediately, then the driver of the spread. Presenting the band as the answer, rather than as a hedge on the answer, is what makes it land.

If the forecast reliability of the underlying spend lines has been scored, say so. A runway built on a forecasting process with a known optimistic bias should be read accordingly, and saying that out loud is what makes the analysis credible.

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

Dividing cash by average burn and presenting the result as fact. Treating restricted cash as available. Building burn from a trailing average that includes a one-time month. Reporting a range without its driver. Giving in and quoting a single date because it feels more confident.
