---
name: orior-credits
description: Check the price of an Orior AI request with quote_price and get a yes before spending credits. Use before any Orior AI video, more than 4 images, 4K images, preset characters, social posts, or whenever the person asks what something costs or how many credits they have.
---

# Confirm the cost before spending Orior AI credits

Orior AI tools spend credits from the same balance as the Orior AI app. Prices change, so never quote them from memory. Checking is free.

## Check

- `get_account`: plan and credit balance.
- `quote_price`: the price of one request without running it. Pass `type` (`image` or `video`) and only the settings that change the price: for an image the `resolution`, for a video the `model`, `duration` and `resolution`, for example `{ "model": "kling-3.0", "duration": "10", "resolution": "1080p" }`. No prompt or photo is needed. For a motion control video, also pass `motion_video_seconds`.
- `list_models`: every video model with its allowed settings and prices.
- `get_usage`: credits spent this month, by day.

## Ask first

Tell the person the price in credits and their balance, then wait for a clear yes before:

- any video
- more than 4 images in one go
- 4K images
- a character from a preset
- a social post, and connecting a social account beyond the plan allowance (`create_social_connect_link` returns `monthly_fee_credits`)

A single image at the default settings can go ahead without asking when the request is clear.

A new account that connected from a chat may have welcome credits for one 1K image. Use them on the image the person most wants, with their character, not on a test.

Write it plainly, for example: "This video costs <price> credits. You have <balance>. Go ahead?"

## When something goes wrong

- Not enough credits: the error says how many are needed and links to the page where credits are added. Pass both on as a clickable link, say that nothing was charged, and offer to run the same request once credits are added. Do not lower the quality to fit unless the person asks.
- Plan limits: the Free plan holds 1 character and makes one image a minute here, so ask for images one after another. A limit error says what to do: wait for the running job, delete a character, or pick a bigger plan from the link it gives.
- Spending limit: `set_credit_limit` sets how many credits this connection may spend a month. It can set a first limit or lower it; only the person raises or removes it, in Dashboard → MCP. Offer it before any scheduled task.
- Failed and cancelled generations are refunded automatically (`refunded_credits`).
- `cancel_generation` works only while a job is still queued, and refunds it. A job that already started finishes on its own and is refunded if it fails; do not try to cancel it again.
- If a generate call times out without a generation ID, calling it again with the same arguments within 10 minutes returns the first job instead of charging twice. `list_generations` also shows it.
- To check on a running job use `get_generation`. Never start a new generation to check.
