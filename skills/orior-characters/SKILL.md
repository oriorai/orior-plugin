---
name: orior-characters
description: Pick a saved Orior AI character or create a new one before making images or videos. Use when the person names a character, asks for "my character", or wants a new consistent AI person from face photos or a ready made preset.
---

# Pick or create an Orior AI character

Every Orior AI image or video that features a person works best with a saved character. A character keeps the same face across every image and video, so find or create one first and pass its ID as `character_id`.

## Find a saved character

1. Call `list_characters`. It returns each character's ID, name and photos.
2. If the person named a character, match it by name. If two match, or none do, show the list and ask.
3. Show characters as a short numbered list in plain text, for example `1. Mila (photo link)`. Do not paste raw IDs unless the person asks.
4. Use the chosen ID as `character_id` in every later call. Never upload the face photos again for a saved character.

## Create a character from face photos

Use `create_character` when the person has photos of the face they want. It is free.

- `name`: up to 30 characters. `gender`: `male` or `female`.
- `images`: 1 to 3 photos of the same face. Put a clear front view first; more angles improve the likeness.
- Photos can be upload IDs (see the `orior-upload-files` skill), public https links or data URLs.
- Optional `voice_key` from `list_voices`, for narrated videos.

Only create a character from the person's own face or from someone who agreed to it. Do not create characters of minors, celebrities or other public figures. Orior AI refuses these.

## Create a character from a preset

Use this when the person has no photos and wants a new look.

1. Call `list_character_presets`. Show a few options that fit what they described, each with its name and portrait link.
2. Ask them to pick one and give a name (up to 20 characters).
3. Customizable presets also take `customization`: `skin_tone` (light, medium), `hair_color` (black, brown, blonde), `eye_color` (brown, green, blue), `body_type` (slim, average, athletic), `age_range` (young, middle, mature). Ask only about the ones they care about.
4. Creating from a preset costs credits. Say so and wait for a yes, then call `create_character_from_preset` with `name` and `base_id`.
5. Offer a first portrait with `generate_image` and the new `character_id`.

## Change or remove a character

- `update_character` renames a character or changes its voice.
- `delete_character` is permanent. Ask for a clear yes first. Images already made stay in the library.
