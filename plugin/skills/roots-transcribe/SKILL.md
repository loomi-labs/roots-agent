---
name: roots-transcribe
description: "Read a scan, a church record or a letter in roots: mark each line or entry on the page and save the reading of each mark. Use when the user asks to read, transcribe or mark a scan or a document."
compatibility: Needs the roots MCP server (Streamable HTTP with OAuth).
metadata:
  scope: research
  tools: list_media get_media get_media_file view_marks edit_marks list_readings add_reading
  write-tools: accept_reading
---

# Read a scan with roots-transcribe

This skill needs the `research` scope. The optional last step needs the `write` scope.

## Steps

1. Find the item. Call `list_media` or `get_media`.
2. Look at the page. Call `get_media_file` for the image. Call `view_marks` with `grid` and `region` to zoom in and to read the position of a line as a fraction of the page.
3. Mark each line or entry with `edit_marks`. Use a box for a word or a face and a band for a line. Positions are fractions of the page. Use `rotation` for a slanted line. In the `research` scope `edit_marks` makes a proposal and gives no mark ids. Put the text of each line into the `transcription` of the proposed mark. In the `write` scope `edit_marks` applies the marks at once and gives their ids.
4. Save a reading with `add_reading` only on a mark that exists. Get the mark id from `view_marks`, from the ids of `edit_marks` in the `write` scope, or after an admin approves the proposal. Write the text as written: no modern spelling. Write `[?]` for an unclear word. Add a confidence.
5. Call `list_readings` to compare readings of the same mark.
6. With the `write` scope, call `accept_reading` for the best reading. It sets the transcription of the mark. A mark with an event then gets its citation. In the `research` scope the admin accepts the reading.

## Rules

- Check each mark with `view_marks` after you add it.
- Do not guess a word. Mark it `[?]`.
