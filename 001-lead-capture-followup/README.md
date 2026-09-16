# 001: Lead Capture and Follow-up

**Sector:** General
**Technique:** Google Sheets trigger, conditional branching, Telegram + Gmail notification, scheduled digest
**Built:** August 31, 2026
**Cost solved:** Leads going quiet with no follow-up system. Most deals aren't lost to a bad pitch, they're lost to silence after the first contact.

## How it works

Two separate n8n workflows, kept apart deliberately so a real-time intake issue never blocks the daily digest, and each has its own execution history to debug independently.

**Workflow 1: Lead Intake & Notification**
1. Google Sheets Trigger (Row Added) watches the Form Responses sheet for new submissions
2. Edit Fields maps the raw form fields into the Leads schema (Name, Contact, Sector, Interest note, Stage, dates)
3. Append Row in Sheet writes the mapped record into the Leads database
4. A Telegram node sends me an immediate ping with the new lead's details
5. An If node checks the contact type and routes the acknowledgment: Gmail for an email contact, Telegram for a phone contact

**Workflow 2: Daily Follow-up Digest**
1. Schedule Trigger fires once daily
2. Get Row(s) in Sheet reads the full Leads database
3. A Code node (Python) filters to rows where Next Follow-up Date is today or earlier and Stage isn't Client, Retainer, or Lost, then builds a single summary message, always producing exactly one output so an empty day still sends "No follow-ups due today" instead of going silent
4. Telegram sends the digest

## Stack

n8n (self-hosted, Docker), Google Sheets, Gmail, Telegram Bot API

## Result

Launched today, no lead volume yet to report. Update this section after the first week of real submissions with: leads captured, response time, anything that broke in production that didn't show up in testing.

## Reuse notes

To adapt this for a client: swap the Telegram channel for WhatsApp Cloud API once business verification is in place, since that's the channel Kenyan SME and NGO contacts actually expect. The Sheets database can move to Airtable or Postgres at higher volume without changing the workflow logic, only the read/write nodes.

## Demo

LinkedIn: [add link once posted]
Shortform (TikTok/Shorts/Instagram): [add link once posted]
