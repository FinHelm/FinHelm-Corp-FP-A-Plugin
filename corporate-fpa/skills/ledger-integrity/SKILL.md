---
name: ledger-integrity
description: Check whether a ledger is clean enough to report from, before anyone builds a dashboard on it. Use when someone asks about data integrity, missing dimensions, duplicate invoices or references, zero-price lines, unusual transactions, or whether the numbers can be trusted yet. Produces counts and lists for review, never a financial figure and never a verdict on a record.
---

# Ledger integrity

Reporting is only as good as the ledger under it. A team that has just connected an assistant to its ledger usually wants a dashboard first; the better first question is whether the posted transactions carry what the dashboard will group by. This skill asks that question in a way the assistant can answer honestly: by counting and listing, never by judging.

Nothing here computes a financial value, and nothing here calls a record wrong. A flagged record is a record for review by the person who owns the journal it sits in. Some zero-price invoices are legitimate. Some repeated purchase-order numbers are deliberate. The work is to surface them with their counts and let a person decide.

## Step 1. Establish the scope with the person, in writing

Do not assume what a clean transaction looks like. Ask, and record the answers at the top of the report so the next run uses the same scope.

- **Required dimensions, per transaction type.** Which dimensions must every posted line carry: for example class, warehouse and customer on sales transactions. The person names them; the skill never supplies a default list, because every company's reporting dimensions are its own.
- **Journals the rule applies to.** Payroll, fixed-asset, allocation and consolidation journals legitimately carry none of the reporting dimensions. The person says which journals or transaction types the check covers. A journal the person excluded is never scored.
- **Period and entities.** Which periods, which entities, and whether private entities are included. Say it explicitly on every query.
- **Reference fields.** Which field carries the customer's purchase-order number in this company (on Order Entry documents it is usually the customer PO number field; on receivables invoices it is often the reference number), and which document types count as invoices.

## Step 2. Validate the schema before every query

Read the object definition for each object you will query before you query it, and use only the field names it returns. Field names differ between objects and between header and line records. Request text output rather than structured content so the records themselves are visible, not just counts. Never guess a field name and never reuse one from a different object.

## Step 3. Count first, then list

For each check, run the aggregate first (a count grouped by journal, period or entity), then page through the flagged records to completeness and state the total count beside the list. A count tells the person where the problem concentrates; the list tells them what to open. Never present a list without its count or a count without saying whether paging reached the end.

## Step 4. The checks

**A. Posted lines missing a required dimension.** On posted journal-entry lines within the scoped journals, periods and entities, count lines where any required dimension is empty, grouped by journal; then by account and period for the journals that matter. One query with a compound filter (posted, and any of the required dimensions empty) answers the count; the grouped form shows where the gaps concentrate. Report missing dimensions per journal, never as a single company-wide number, because a journal that legitimately carries none of them would swamp the figure.

**B. Repeated customer references.** On invoices within scope, group by customer and reference field and count; a count above one is a flag. List each repeated pair with its invoice numbers and dates. A repeat may be a legitimate split shipment, a credit and rebill, or a duplicate; say which the person should check and do not decide.

**C. Zero-price lines.** On Order Entry document lines of the invoice types in scope, flag lines with a unit price of zero and a quantity above zero. On receivables invoice lines, which carry amounts rather than prices, group zero-amount lines by account and by invoice first: structural lines (tax, discount, subtotal) often post at zero on a few accounts, and the person will recognise those accounts at once. Exclude the accounts the person names as structural, then list what remains. A naive zero filter that skips this step flags the tax lines on every invoice and buries the real cases.

**D. Duplicate master records, optional.** Customers, vendors or items whose names match ignoring case and punctuation, or whose identifiers differ only by a suffix. This is a list for review, not a merge instruction; merging is a configuration change that belongs to the administrator.

## Step 5. Reconcile the scope before reporting

Header and line objects do not always scope entities the same way: a header query from the top level can return one record while the corresponding line query returns thousands, because private entities are included on one path and not the other. Before reporting any count, run the matching header count with the same entity scope and confirm the two agree. If they do not, say so and fix the scope before anything else.

## Step 6. Report for review, never for judgement

Open with the scope as agreed in Step 1. Then one short table per check: scope, records examined (the total, paged to completeness), records flagged, and where they concentrate (journal, account, period, entity). Then the lists, with document identifiers and dates and no amounts unless the person asked for them. Close with who should look at each list: the owner of the journal, the person who keys the invoices, the administrator for master records.

Use "for review" throughout. Do not write "error," "wrong," "bad data" or "dirty"; the ledger belongs to the person reading the report, and a flagged record is a question, not a finding.

## Step 7. Keep the scope file and rerun

Save the Step 1 scope with the report. The next run uses the same scope so the counts are comparable month to month, and the trend in flagged records is the measure of whether the clean-up is working. If the scope changes, say so and do not compare across the change.

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

Supplying a default list of required dimensions instead of asking. Scoring a payroll or fixed-asset journal the person excluded. Reporting a company-wide count of missing dimensions that one journal dominates. Filtering zero amounts without first separating structural lines by account. Calling a repeated reference a duplicate instead of listing it for review. Presenting a list without its total or a count without saying whether paging finished. Mixing a header count from one entity scope with a line count from another. Pasting record links into the report. Writing "error" or "wrong" about a record nobody has looked at.
