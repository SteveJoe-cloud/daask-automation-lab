# 002: Overdue Invoice Reminder

**Sector:** SME
**Technique:** Scheduled check, validation and rejection logging in code, Switch routing across four message types
**Built:** September 2026
**Status:** Complete

## Cost solved

Unpaid invoices sitting untracked with no consistent follow-up, a common SME cash flow leak, made worse without a documented eTIMS-compliant paper trail on reminders.

## How it works

1. An Invoices sheet holds Client Name, Client Contact, Invoice Number, Amount (KES), Due Date, Status
2. Schedule Trigger fires daily at 8am, Get Row(s) reads the full sheet
3. A Code node validates each row (checking for a parseable due date and an "unpaid" status), calculates days overdue, and separates valid overdue invoices from rejected rows (bad dates, future due dates, or already paid), logging the rejection reason for each
4. Contact type is checked automatically: an "@" in the contact field routes to email, anything else routes to Telegram
5. A Switch node splits the output into four paths: reminder_email, reminder_telegram, escalation (14+ days overdue), and summary
6. Reminders reference eTIMS compliance directly, noting the invoice has already been transmitted to KRA and offering to resend the compliant copy

## Stack

n8n (self-hosted), Google Sheets, Gmail, Telegram Bot API, Code node (JavaScript)

## Result

Rejected rows are logged with a specific reason (invalid date format, future due date, or wrong status) rather than silently dropped, which makes the daily summary message useful for catching data-entry problems in the Invoices sheet itself, not just tracking overdue payments.

## Reuse notes

The 14-day escalation threshold and the eTIMS-specific wording in the reminder are both easy to expose as configurable values for a client with different follow-up norms or no eTIMS obligation.

## Demo

[add link once posted]
