---
name: orior-credits
description: Check the price of an Orior AI request with quote_price and get a yes before spending credits. Use before any Orior AI video, more than 4 images, 4K images, preset characters, social posts, or whenever the person asks what something costs or how many credits they have.
---

# Confirm the cost before spending Orior AI credits

Orior AI tools spend credits from the same balance as the Orior AI app. Prices change, so never quote them from memory. Checking is free.

## Check

- `get_account`: plan and credit balance.
- `quote_price`: the price of one request without running it. Pass `type` (`image` or `video`) and `request` with the same fields you would send to `generate_image` or `generate_video`, for example `{ "model": "kling-3.0", "duration": "10", "resolution": "1080p" }`. An image request needs at least a prompt, character, scene image or product, as in the real call. For a motion control video, also pass `motion_video_seconds`.
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

Write it plainly, for example: "This video costs <price> credits. You have <balance>. Go ahead?"

## When something goes wrong

- Not enough credits: the error says how many are needed and links to the page where credits are added. Pass both on. Do not lower the quality to fit unless the person asks.
- Failed and cancelled generations are refunded automatically (`refunded_credits`).
- `cancel_generation` works only while a job is still queued, and refunds it.
- If a generate call times out without a generation ID, calling it again with the same arguments within 10 minutes returns the first job instead of charging twice. `list_generations` also shows it.
- To check on a running job use `get_generation`. Never start a new generation to check.
