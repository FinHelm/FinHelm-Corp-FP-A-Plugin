# Corporate FP&A

Skills and commands for financial planning and analysis inside an operating company: the office of the CFO, not the sell side or the buy side. The questions are "what will we spend next quarter, how confident should we be, and what do I tell the board," and the discipline is that no figure appears without a receipt.

Version 0.1.2. Apache 2.0. Maintained by FinHelm Corp.

## What this adds

| Skill | Command | Description |
| --- | --- | --- |
| forecast-reliability | `/forecast-score` | Score how much a forecast can be trusted, against its own history |
| variance-decomposition | `/variance` | Decompose budget-versus-actual variance into the drivers that caused it |
| cash-runway | `/runway` | Cash runway as a range with confidence bands, not a single date |
| driver-sensitivity | `/drivers` | Rank which inputs actually move the forward number |
| scenario-construction | `/scenario` | Build defensible base, upside, and downside cases |
| board-package | `/board-pack` | Board-ready financial narrative that presents a range without losing the room |

## Architecture

Skills carry method. Connectors carry computation. This split is deliberate and load-bearing.

Every skill here describes how to run the work: what to gather, how to sequence it, what good looks like, how to present it, and where practitioners commonly go wrong. None of them calculate a financial value. Numbers come from a computation tool that reads the ledger itself and returns a receipt, so that every figure traces to the ledger and an auditor can follow the path.

Install the skills alone and you get a practitioner's method and a set of honest refusals. Add the computation connector with a ledger it can read, and you get numbers.

## Connecting a ledger

This plugin does not build ERP connectors. It reads the one Sage Intacct publishes: a read-only MCP server in Sage's AI Gateway, governed by Intacct roles. That is the only ledger read path verified in this release. Other vendors' MCP servers can be added by the person installing; nothing here has been tested against them.

The `finhelm` connector computes the reliability, distribution, bridge and sensitivity figures the skills reference. It requires a FinHelm account, reads the ledger itself through a FinHelm-connected ledger, and returns results with receipts. In this release it computes from QuickBooks Online and DualEntry; Sage Intacct follows with FinHelm's Intacct connector.

**What that means on a Sage Intacct install today.** The skills run the method, read through Sage's connector for discovery, and stop at "requires the connector" rather than computing a forecast, a bridge, a range or a reliability band inline. Numbers Claude reads through Sage's connector are discovery, not readings. These skills never instruct the assistant to pass values read through Sage's connector into FinHelm's tools, and no FinHelm sign-in is needed to use them this way. That is a statement about what the skills instruct, not about everything the assistant processes or retains, which is governed by the terms of the Claude plan in use and by Sage's terms for the Gateway.

## Installing

**Claude Code.** Add this repository as a marketplace and install the plugin:

```
/plugin marketplace add FinHelm/Corp-FP-A-Plugin
/plugin install corporate-fpa@finhelm
```

The six commands become available. Both connectors in `.mcp.json` are registered; each asks you to sign in the first time it is used, and you can leave the `finhelm` connector unsigned if you only want the method and the Sage read path.

**Claude on the web or Claude Desktop.** Commands are a Claude Code feature; here the skills are used by asking in plain language ("score the reliability of our operating expense forecast", "decompose the Q3 variance"). Two steps:

1. Add the Sage Intacct connector in Claude's connector settings as a custom connector with the URL from `.mcp.json` and the OAuth client ID and secret your Intacct administrator created in Sage's developer portal. Sign in with Sage-hosted sign-in. Each person signs in individually.
2. Upload the six skills. Each folder under `skills/` is one skill; zip each folder (the zip contains `SKILL.md` at its root) and add it in Claude's skills settings. Enable the ones you want.

Menu names move between releases of Claude; if yours differ, the two steps are the same: one connector, six skills.

**Before you connect.** The Intacct administrator creates the OAuth client against an AI-enabled sender ID and a read-only role scoped to what the finance team should see. The role decides what the assistant can read. Keep a record of what was connected, by whom, and when, and know how to revoke it.

## Working on the Sage Intacct AI Gateway: rules the skills follow

These come from verification on a non-production Intacct company, not from documentation, and every skill carries the same paragraph. Put them in your project instructions too, because the assistant does not keep what it learned last week unless it is written where it loads every session.

- Page to completeness. The Gateway returns at most 100 records per page, with a flag that says whether more remain and a total count. Sum nothing until the flag is false, and state the total count beside any sum.
- Actuals are posted entries from the operating accrual book. Journal-entry lines carry no book identifier; the book lives on the journal. Exclude consolidation books, adjustment journals and the Commitments book, or the figure is not an actual.
- State the grain before any comparison: account, entity, period, and only the dimensions populated on both sides. A budget at one department and actuals at another is a mismatch of grain, not a variance.
- Name the entities in scope. Multi-entity queries from the top level skip private entities unless include-private is set; say which you intend, and never present a consolidated figure that is missing an entity.
- Take the entity scope from the person or from the computation tool, never from a list on Sage; the Gateway exposes no entity master.
- Periods come from the reporting calendar when the line's period is empty; say which calendar.
- A line's base currency is the book's, not necessarily the entity's. Anything that crosses currencies needs a named translation basis or is refused.
- Request text output: call Sage's tools with `useStructuredContent` set to false, or the model works from counts and summaries rather than records.
- Every record and query result carries web links into the company. They are not data. Keep them out of anything written, pasted, logged or shared.

## Telling us what went wrong

The most useful feedback is three lines: the question you asked, what the assistant did, and where it went wrong. Open an issue on this repository with those three lines and no ledger data. Do not paste records, amounts, links or company identifiers.

## Nothing here is advice

These skills draft analyst work product for review by a qualified professional. They do not make investment recommendations, execute transactions, post to a ledger, or approve anything. Every output is staged for human sign-off. Forecast reliability scoring describes the historical behavior of a forecasting process; it is not a guarantee about the future.

## License

Apache 2.0; see `LICENSE`. "FinHelm" and FinHelm's product names and marks are trademarks of FinHelm Corp and are not licensed under the Apache License; see `NOTICE`.
