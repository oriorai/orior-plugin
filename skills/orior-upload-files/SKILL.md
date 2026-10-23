---
name: orior-upload-files
description: Upload a local photo, video or audio file to Orior AI with create_upload_url, curl and finish_upload. Use when the person wants to use a file from their workspace or chat attachments (a face photo, a pose photo, a product photo, a motion clip) with the Orior AI tools.
---

# Upload a local file to Orior AI

Orior AI tools take media as an upload ID (`upl_...`), a public https link or a data URL. A local file path does not work as a media input.

## Before uploading

- If the file is already at a public https link, pass the link directly. No upload needed.
- Grok Bot keeps attached files in its cloud workspace and Cursor works in the project folder. Find the file there.
- If you cannot run shell commands, ask the person for a public link instead.
- `open_upload_box` shows an upload box in some apps only. In Grok Bot and Cursor use the steps below.

## Steps

1. Read the file type and size:

   ```bash
   file --mime-type -b "photo.jpg"
   wc -c < "photo.jpg"
   ```

   Accepted: images (png, jpeg, webp, heic, heif, gif) up to 20 MB, videos (mp4, mov, webm, m4v) up to 200 MB, audio (mp3, m4a, aac, wav, ogg, webm) up to 50 MB.

2. Call `create_upload_url` with `content_type` (for example `image/jpeg`) and `size` in bytes. It returns `id`, `upload_url` and `upload_headers`.

3. Send the raw bytes within 15 minutes, using the same content type:

   ```bash
   curl -sS -X PUT -H "Content-Type: image/jpeg" --upload-file "photo.jpg" "<upload_url>"
   ```

   Quote the URL; it is long and signed. An empty reply with no error means it worked.

4. Call `finish_upload` with the `id`. The upload is ready when it answers with status `ready`.

5. Use the `upl_...` ID as the media input: `photo`, `images`, `scene_image`, `start_frame`, `reference_images` or `motion_video`.

Uploads stay available for 7 days. For several files, repeat steps 2 to 4 for each one.

## If something fails

- The URL expired: start again from step 2.
- The size or type was refused: tell the person the limit above.
- Never send a whole file as a data URL in the chat when it is more than a small image.
