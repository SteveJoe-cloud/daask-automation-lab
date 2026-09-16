# 002: Overdue Invoice Reminder

**Sector:** SME
**Technique:** Scheduled check, Code node filtering, Switch routing to separate client-facing and internal messages
**Built:** September 2026
**Status:** In progress. Core logic built and code written, last known state was debugging a Switch/If branch showing "node was not executed," which is expected behavior when a branch legitimately receives zero matching items rather than a bug. Needs a confirmed end-to-end test with real overdue data before marking complete.

## Cost solved

Unpaid invoices sitting untracked with no consistent follow-up, a common SME cash flow leak, especially relevant with eTIMS compliance in view.

## How it works

1. An Invoices sheet holds Client Name, Client Contact, Invoice Number, Amount (KES), Due Date, Status, Last Reminder Sent
2. Schedule Trigger fires daily, Get Row(s) reads the full sheet
3. A Code node filters to Unpaid invoices with a Due Date today or earlier, builds one reminder message per client plus an escalation flag for anything 14+ days overdue
4. A Switch node routes reminder-type items to a Gmail node (client-facing) and escalation/summary items to Telegram (internal, to me)

## Stack

n8n (self-hosted), Google Sheets, Gmail, Telegram Bot API, Code node (JavaScript, with a Python variant also written)

## Reuse notes

The 14-day escalation threshold is hardcoded in the Code node, easy to expose as a configurable value for a client with different follow-up norms.

## Demo

Not yet recorded, pending confirmed test pass.
