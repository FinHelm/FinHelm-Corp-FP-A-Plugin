---
description: Check whether the ledger is clean enough to report from
---

Run the ledger-integrity skill.

Establish the scope first and write it at the top of the report: the required dimensions per transaction type as the person names them, the journals the rule applies to, the periods and entities with private entities stated, and the reference field that carries the customer's purchase-order number. Supply no defaults.

Validate each object's schema before querying it and request text output. Count first, grouped by journal, then page through the flagged records to completeness and state the total beside every list. Reconcile header and line counts at the same entity scope before reporting.

Report every flagged record as for review, never as an error. No amounts in the report unless asked. No record links anywhere.

$ARGUMENTS
