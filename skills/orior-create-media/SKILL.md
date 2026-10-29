---
name: orior-create-media
description: Choose the right Orior AI tool for an image or video of a character. Use when the person wants their Orior AI character in a photo they shared, a new scene, a product shot, an edit, or a video, so the request goes to place_character_in_photo, generate_image or generate_video with the right inputs.
---

# Make an image or video with Orior AI

Pick the tool from what the person brings, not from the words they use.

## Which tool

| The person wants | Tool and inputs |
| --- | --- |
| Their character in a photo they shared: "copy this pose", "recreate this", "put her in this" | `place_character_in_photo` with `character_id`, the photo as `photo`, and only the differences in `changes` |
| A new scene described in words | `generate_image` with `character_id` and a `prompt` (subject, action, setting, camera, light) |
| The character holding or showing a product | `generate_image` with `character_id` and `product_id` (from `list_products`, or save one with `create_product` from 1 to 3 photos, free) |
| A change to an existing image, no character swap | `generate_image` with the image as `scene_image` and `edit: true` |
| A video | `generate_video`, see below |

Rules that keep the result right:

- The photo whose pose, framing and setting should be kept is always the `photo` (or `scene_image`). Never send it in `reference_images`.
- `reference_images` are only for extra details such as an outfit or an object. Tag each one (`@ref1`, `@ref2`, up to 6) and mention the tag in the prompt or `changes`.
- `changes` should say only what differs from the photo, for example "wearing a red dress". Leave it empty to copy the photo as it is.
- Defaults are 9:16 and 1K. Use 4K only when asked; it costs more.
- Earlier results work as inputs: pass a result URL, or a URL from `list_library` for anything made in the Orior AI app.

## Videos

1. Call `list_models`. Each model lists its allowed durations, resolutions, aspect ratios and whether it makes sound.
2. Pick a model that fits, and check the price with `quote_price` (see the `orior-credits` skill). Videos cost much more than images, so wait for a yes.
3. For a character video, make the first frame with `generate_image`, show it, then call `generate_video` with that image as `start_frame`.
4. Videos usually take 1 to 5 minutes.

## Waiting for results

- A generate call waits up to the time the server instructions give (45 seconds in most apps, longer in Grok Bot). If the result is not ready, it returns a generation ID (`gen_...`).
- Then call `get_generation` with that ID and `wait_seconds` (up to 240) until the status is completed, failed or cancelled.
- Never call a generate tool again to check on a running job. `get_generation` never charges.
- When it is done, give the full size link (`result.url`). In Grok Bot, show a finished image in the reply as a Markdown image, `![short description](result.url)`; videos stay links.
- Failed and cancelled generations are refunded automatically. Pass the error message on. If a request is blocked for content, do not reword it to get around the block.

## Apps without cards

`open_creation_card` and `open_upload_box` show interactive cards in Claude and ChatGPT only, and Grok Bot does not get them. There, confirm the character, photos and settings in plain text, then call the tool yourself. For the person's own photos, see the `orior-upload-files` skill.

## After the first image

Offer one concrete next step with its price: the same character in other places or outfits, a short video from that image (`start_frame`), or a daily post (see the `orior-daily-posts` skill).
