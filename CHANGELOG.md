# Changelog

## 0.2.1, 29 October 2026

- Published as the FinHelm Corp FP&A plugin. Plugin identifier is now `finhelm-corp-fpa` and the install path points at this repository. No change to any skill, command or connector.

## 0.2.0, 28 October 2026

- New skill and command: ledger-integrity, `/integrity`. Checks whether a ledger is clean enough to report from: posted lines missing a required dimension, repeated customer references, zero-price lines, and duplicate master records. The person sets the scope; the output is counts and lists for review, never a financial figure. Runs without the computation connector.

## 0.1.2, 28 October 2026

- Rules for reading a ledger through the Sage Intacct AI Gateway, in every skill and in the README.
- board-package: every figure comes from the computation tool's result and its receipt.
- Connector descriptions: what the FinHelm connector computes from and retains; what the Sage Intacct connector requires to connect.
- README: installation for Claude Code and for Claude on the web or Desktop; what an Intacct-only install does; feedback guidance; trademark notice.
- Repository: LICENSE, NOTICE, marketplace manifest, this changelog.

## 0.1.1, 14 October 2026

- variance-decomposition: basis check (one named book, posted entries only, same grain) and the computation-tool clause.

## 0.1.0, 13 August 2026

- Initial release: six skills, six commands, two connectors.
