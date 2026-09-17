# 004: Lexi, Telegram AI Assistant

**Sector:** General
**Technique:** LangChain agent node, Qwen via DashScope (OpenAI-compatible endpoint for chat, native Qwen ASR for voice), tool use (Baserow, Google Calendar, Gmail)
**Built:** September 2026
**Status:** Complete

## Cost solved

A single Telegram-based assistant that can answer questions against tasks (Baserow), contacts (Baserow), calendar events (Google Calendar), and email (Gmail) without opening four separate apps, by text or by voice.

## How it works

1. Telegram Trigger listens for incoming messages, an AllowList/If check restricts access to a single authorized chat ID
2. Text and voice messages are routed differently
3. Voice messages are fetched from Telegram, base64-encoded, and sent to Qwen's native ASR model (qwen3-asr-flash) for transcription, resolving the earlier plan to rely on OpenAI Whisper
4. The agent (Lexi) runs on a Qwen chat model via DashScope's OpenAI-compatible endpoint, with a buffer memory for conversation context
5. Baserow (tasks, contacts), Google Calendar, and Gmail are wired in as tools the agent can call
6. The response is sent back to the same Telegram chat

## Stack

n8n (self-hosted), Telegram Bot API, DashScope/Qwen (chat and ASR), Baserow, Google Calendar API, Gmail API

## Result

Voice messages now transcribe entirely on Qwen's own infrastructure rather than mixing providers, one less external dependency and one less credential to manage.

## Demo

[add link once posted]
