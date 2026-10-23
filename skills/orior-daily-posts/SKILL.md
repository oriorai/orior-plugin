---
name: orior-daily-posts
description: Plan, create and schedule daily social posts for an Orior AI character with publish_social_post. Use when the person wants their Orior AI character to post on Instagram, TikTok, YouTube, Threads or X, today or as a routine for the coming days. Social posting needs a paid Orior AI plan.
---

# Daily posts for an Orior AI character

Orior AI can publish images and videos to a character's own social accounts, now or at a set time. Posts are public, so nothing goes out without the person's yes on the exact post.

## Before you start

- Social posting is for paid Orior AI plans. If `list_social_accounts` or `create_social_connect_link` is not available, or answers that the plan does not allow it, tell the person it needs a paid plan and stop.
- Call `list_social_accounts` with the `character_id`. If a platform they want is missing, call `create_social_connect_link` and give them the link. The account owner opens it and signs in to the platform. If it shows `monthly_fee_credits` above 0, say so first.
- Platforms: `instagram`, `tiktok`, `youtube`, `threads`, `twitter` (X).

## One day's post

1. Agree on the idea, the platforms and the time. Use the person's time zone and confirm it.
2. Make the content with the Orior AI tools (see `orior-create-media`). Only results made through these tools have the generation IDs a post needs. One post holds one video or up to 10 images.
3. Write a short caption in the character's voice. Keep links out of X captions unless asked; they cost more.
4. Show the person, in plain text: the image or video links, the caption, the platforms, the time and the price (see `orior-credits`). Wait for a clear yes.
5. Call `publish_social_post` with `character_id`, `platforms`, `generation_ids`, `caption` and `scheduled_at` (ISO 8601 with offset, at least 5 minutes ahead). Leave `scheduled_at` out to post now.
6. Platform options go in `settings`, for example `{ "instagram": { "content_type": "reel" } }` or `{ "youtube": { "title": "..." } }`.
7. Check the result with `get_social_post`. Failed platforms are refunded.

## A routine for the coming days

- Plan the whole run at once: one line per day with the idea, the platform and the time. Get a yes on the plan.
- Make each day's content, then show all posts together with the total price before scheduling.
- Schedule each day as its own `publish_social_post` with its own `scheduled_at`.
- Keep the same character and a consistent look; vary place, pose and moment so the feed feels real.
- `list_social_posts` shows what is scheduled and what went out.

## Never

- Post or schedule without a yes on the final content.
- Change a caption, platform or time after the yes without asking again.
