# Changelog

## 0.1.2, 28 October 2026

- Gateway rules: one identical section, "Reading from the ledger through the Sage Intacct AI Gateway", added to all six skills and to the README. Page to completeness and state the count; posted entries from the operating accrual book only; grain before any comparison; entity scope named, private entities explicit; entity scope from the person or the computation tool, never from Sage; periods from the reporting calendar; base currency is the book's; text output requested from Sage's tools; response links never carried into outputs.
- board-package: computation-tool clause added (every figure from the tool's result and receipt; no inline ranges or bands), plus a matching common failure.
- plugin.json: description no longer lists a close-review skill that does not ship; version 0.1.2; keyword sage-intacct.
- .mcp.json: the finhelm connector keeps the live host and now describes what it computes from in this release, what it retains, and that the skills never pass values from another connector into it; the sage-intacct connector states the OAuth client requirement, per-person Sage-hosted sign-in, structured-content default and the 100-record page.
- README: installation for Claude Code and for Claude on the web or Claude Desktop (one connector, six skills); the Business Central claim removed as unverified; the "point .mcp.json at whichever your client runs" line removed; what an Intacct-only install does and does not do; feedback template; trademark notice.
- Repository: LICENSE, NOTICE, marketplace manifest, this changelog.

## 0.1.1, 14 October 2026

- variance-decomposition: basis check (one named book, posted entries only, same grain) and the computation-tool clause with the refusal path "the bridge requires the connector"; matching common failure.

## 0.1.0, 13 August 2026

- Initial release: six skills, six commands, two connectors.
