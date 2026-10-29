# Orior AI plugin for Grok Bot and Cursor

Orior AI creates photorealistic images and videos of consistent AI characters: the same face in every photo and video, optionally holding your real products, ready to post to the character's own social accounts. This plugin connects Grok Bot and Cursor to the hosted Orior AI MCP server and adds skills that guide the agent through the main flows.

The repository holds only manifests, skills and a logo. It ships no scripts, hooks or binaries and stores no credentials.

## What you can do

- Save a character from 1 to 3 face photos, or pick a ready made preset.
- Put your character into any photo you share: the pose, camera angle, framing and setting are kept and the person is swapped for your character.
- Create new scenes from a description, with the character holding or showing a saved product.
- Turn an image into a video with one of several video models, with sound on the models that support it.
- Upload photos and clips from your workspace.
- Post or schedule images and videos to the character's Instagram, TikTok, YouTube, Threads and X accounts, or let the character post every day with a scheduled task (paid plans).
- Check your credits and the price of a request before anything runs.

## Connect

### Grok Bot

1. Find Orior AI in the Grok Bot plugin list and add it, or ask Grok Bot to add the Orior AI plugin.
2. Grok Bot opens an Orior AI sign in page. Sign in or create an account, review the access the app asks for and approve it.
3. Ask for something, for example: "Show my Orior AI characters" or "Put Mila into this photo".

### Cursor

1. Open the Cursor plugin marketplace, search for Orior AI and add it.
2. The first time a tool runs, Cursor opens an Orior AI sign in page in your browser. Sign in and approve.
3. Ask in the agent chat, for example: "Make a photo of Mila having coffee in Lisbon with Orior AI".

### Sign in

Orior AI uses OAuth: you sign in with your Orior AI account in the browser and approve access. There is no API key to copy. The access covers reading your account and library, creating images, videos, characters and products, and social posting. You can see and remove connected apps at [oriorai.com/dashboard/mcp](https://www.oriorai.com/dashboard/mcp).

### Without the plugin

The same server works as a custom MCP server in any client that supports remote servers with OAuth:

```
https://www.oriorai.com/api/mcp
```

Setup for Claude, ChatGPT, Claude Code and Grok Bot is at [oriorai.com/mcp](https://www.oriorai.com/mcp).

## Credits

- The plugin is free. Images and videos spend credits from your Orior AI balance, the same balance as the Orior AI app.
- A new account that connects from a chat gets credits for its first image. Plans and credit packs are at [oriorai.com](https://www.oriorai.com).
- Reads, uploads, price checks, saving a character from photos and saving products are free.
- The agent checks the price with `quote_price` and asks before videos, larger batches, 4K images, preset characters and social posts.
- Failed and cancelled generations are refunded automatically.
- Social posting needs a paid plan.
- `set_credit_limit` caps what the connection may spend in a month; only you can raise or remove the cap, at [oriorai.com/dashboard/mcp](https://www.oriorai.com/dashboard/mcp).

## Skills

| Skill | What it does |
| --- | --- |
| `orior-characters` | Finds a saved character or creates one from photos or a preset |
| `orior-create-media` | Picks `place_character_in_photo`, `generate_image` or `generate_video` and the right inputs |
| `orior-upload-files` | Uploads local files with `create_upload_url`, curl and `finish_upload` |
| `orior-credits` | Checks prices with `quote_price` and asks before spending |
| `orior-daily-posts` | Plans, creates and schedules social posts with `publish_social_post` |

The skills work in plain text, so they do not depend on interactive cards.

## Contents

- `.cursor-plugin/plugin.json`: Cursor and Grok Bot manifest
- `.grok-plugin/plugin.json`: Grok manifest
- `mcp.json`, `.mcp.json`: the Orior AI MCP server (`https://www.oriorai.com/api/mcp`, Streamable HTTP, OAuth 2.1 with PKCE and dynamic client registration)
- `skills/*/SKILL.md`: workflow skills
- `assets/logo.png`: logo

## Network and data

- MCP server and sign in: `www.oriorai.com`
- Finished images and videos are served from Google Cloud Storage (`storage.googleapis.com`, `firebasestorage.googleapis.com`).
- Uploads use a temporary signed URL on Google Cloud Storage and are kept for 7 days.
- Social posts go to the platforms you connect, only when you approve them.

## Legal and support

- Website: [oriorai.com](https://www.oriorai.com)
- Privacy policy: [oriorai.com/privacy](https://www.oriorai.com/privacy)
- Terms of service: [oriorai.com/terms](https://www.oriorai.com/terms)
- Support: support@oriorai.com

The MIT license covers the files in this repository only. It does not cover the Orior AI service or the media you create with it, which the Orior AI Terms of Service govern. The Orior AI name and logo are not licensed for other use.
