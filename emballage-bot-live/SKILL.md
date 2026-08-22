---
name: emballage-bot-live
description: Build a secure Telegram-driven product-page automation workflow that collects product media and data, renders a branded product page, publishes it through an approved deployment provider, and routes orders through trusted server endpoints. Use when operators need rapid product-page creation from chat.
---

# Emballage Bot Live Reference Skill

Create a Telegram operations bot that turns a structured operator conversation into a product landing page. Treat the chat as an intake interface, not a trusted publishing or payment system.

## Intake state machine

Collect image, product name, price, brand, description, SKU, availability and publication decision in explicit steps. Validate type, length, allowed characters, currency and image dimensions. Persist state in a durable store rather than an in-memory object when restarts matter.

## Safe publishing flow

Generate pages from an escaped template, use safe image URLs or stored media, write only to the approved build/publish location, and return the resulting link to the authorized operator. Keep Telegram tokens and administrator IDs on the server; never emit them into generated HTML or browser JavaScript.

## Order handling

Send order forms to a server endpoint or managed data backend. Validate customer data server-side, rate-limit submissions, apply abuse protection, and notify operators through a server-side bot call. Do not make browsers call Telegram’s bot API with secrets.

## Verification

Test interrupted chats, invalid media, quote escaping, duplicate products, publish failure, unauthorized operator attempts, order validation, and clean-up of expired intake sessions.
