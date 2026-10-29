# Changelog

## 0.2.0, 28 October 2026

- New skill and command: ledger-integrity, `/integrity`. Built from three cases a distribution client reported in its first weeks on the Sage Intacct AI Gateway: posted transactions missing a required reporting dimension, invoices at a zero price, and repeated customer purchase-order numbers. Scope is set by the person (required dimensions per transaction type, journals the rule applies to, periods, entities, reference field); the skill supplies no default dimension list and never scores a journal the person excluded. Counts first, grouped by journal, then lists paged to completeness; header and line counts reconciled at the same entity scope; structural zero-amount lines separated by account before anything is flagged; every flagged record is for review, never an error. Produces no financial figure, so it runs in full without the computation connector.
- Query shapes for checks A and B, and the receivables grouping in check C, run read-only on a non-production Intacct company through Sage's MCP server (counts only). The Order Entry zero-price query and check D are unverified on live data.
- plugin.json description and version; marketplace description; README table, install counts and the Intacct-only statement.

## 0.1.2, 28 October 2026

- Gateway rules: one identical section, "Reading from the ledger through the Sage Intacct AI Gateway", added to all six skills and to the README. Page to completeness and state the count; posted entries from the operating accrual book only; grain before any comparison; entity scope named, private entities explicit; entity scope from the person or the computation tool, never from Sage; periods from the reporting calendar; base currency is the book's; text output requested from Sage's tools; response links never carried into outputs.
- board-package: computation-tool clause added (every figure from the tool's result and receipt; no inline ranges or bands), plus a matching common failure.
- plugin.json: description no longer lists a close-review skill that does not ship; version 0.1.2; keyword sage-intacct.
- .mcp.json: the finhelm connector keeps the live host and now describes what it computes from in this release, what it retains, and that the skills never instruct the assistant to pass values from another connector into it; the sage-intacct connector states the OAuth client requirement, per-person Sage-hosted sign-in, structured-content default and the 100-record page.
- README: installation for Claude Code and for Claude on the web or Claude Desktop (one connector, six skills); the Business Central claim removed as unverified; the "point .mcp.json at whichever your client runs" line removed; what an Intacct-only install does and does not do; feedback template; trademark notice.
- Repository: LICENSE, NOTICE, marketplace manifest, this changelog.

## 0.1.1, 14 October 2026

- variance-decomposition: basis check (one named book, posted entries only, same grain) and the computation-tool clause with the refusal path "the bridge requires the connector"; matching common failure.

## 0.1.0, 13 August 2026

- Initial release: six skills, six commands, two connectors.
