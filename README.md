# FinHelm Corp FP&A plugin

A Claude plugin with seven practitioner skills and commands for the office of the CFO, maintained by FinHelm Corp under the Apache License 2.0.

The plugin lives in [`finhelm-corp-fpa/`](finhelm-corp-fpa/README.md); its README covers what the skills do, how to install them in Claude Code or in Claude on the web and desktop, how the ledger is connected, and the rules the skills follow on Sage Intacct's AI Gateway.

Skills carry method. Connectors carry computation. No skill computes a financial value; figures come from a computation tool that reads the ledger itself and returns a receipt, or they do not appear.

Install in Claude Code:

```
/plugin marketplace add FinHelm/FinHelm-Corp-FP-A-Plugin
/plugin install finhelm-corp-fpa@finhelm
```

Releases are tagged; each release archive of `finhelm-corp-fpa/` is listed with its SHA-256 in `CHANGELOG.md` once cut. Feedback: open an issue with the question you asked, what the assistant did, and where it went wrong; no ledger data.
