# 004: Lexi, Telegram AI Assistant

**Sector:** General
**Technique:** LangChain agent node, Qwen via DashScope (OpenAI-compatible endpoint), voice message transcription, tool use (Baserow, Google Calendar, Gmail)
**Built:** September 2026
**Status:** Workflow built and renamed to Lexi, chat model switched to Qwen. Not yet live, pending creation of the Qwen/DashScope credential in n8n and a decision on the voice transcription path.

## Cost solved

A single Telegram-based assistant that can answer questions against tasks (Baserow), contacts (Baserow), calendar events (Google Calendar), and email (Gmail) without opening four separate apps.

## How it works

1. Telegram Trigger listens for incoming messages, an AllowList/If check restricts access to a single authorized chat ID
2. Text and voice messages are routed differently, voice messages are fetched and transcribed before reaching the agent
3. The agent (Lexi) runs on a Qwen chat model via DashScope's OpenAI-compatible endpoint, with a buffer memory for conversation context
4. Baserow (tasks, contacts), Google Calendar, and Gmail are wired in as tools the agent can call
5. The response is sent back to the same Telegram chat

## Stack

n8n (self-hosted), Telegram Bot API, DashScope/Qwen, Baserow, Google Calendar API, Gmail API

## Known limitation

Voice transcription is still pointed at OpenAI's Whisper endpoint rather than Qwen. DashScope's OpenAI-compatible layer covers chat completions reliably, but its audio transcription sits behind a different, non-OpenAI-compatible endpoint, so this wasn't a safe drop-in swap and was left on the original provider rather than risk silently breaking voice input.

## Demo

Not yet recorded, pending credential setup and a live test.
