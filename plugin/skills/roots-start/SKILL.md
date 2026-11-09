---
name: roots-start
description: Fill an empty or small family tree in roots with persons, families, events and files, with the user as the source of facts. Use when a tree has no or few persons, or when the user says "fill my tree".
compatibility: Needs the roots MCP server (Streamable HTTP with OAuth).
metadata:
  scope: write
  tools: get_guidelines describe_entities search_persons get_chart apply_changes create_proposal create_upload_urls create_media update_guidelines list_changesets revert_changeset
---

# Fill a tree with roots-start

This skill needs the `write` scope. With a `research` grant, `apply_changes` does not exist: send each batch with `create_proposal` and an admin approves it.

Never invent a person or a date. When a fact is missing, ask the user.

## Steps

1. Call `get_guidelines`. Read `start_here` and the rules of the tree.
2. Call `describe_entities` one time. It lists the entities, the fields, the types and the enum values.
3. Ask the user for the persons they know: names, dates, places and relations. Work one generation at a time. Start with the user or with the youngest known person.
4. Before you create a person, call `search_persons` with the name. Do not create a person two times.
5. Create the data with `apply_changes`. Send batches of at most about 50 changes. Give each batch a clear `message`, for example "Add the parents of Anna Beispiel". Use `temp_id` in a create, and `"$<temp_id>"` in later references of the same batch. A batch holds persons, person names, families, family children and events.
6. Write dates in GEDCOM form: `1850`, `ABT 1850`, `BET 1850 AND 1855`, `12 MAR 1850`, `BEF 1900`. A person or a family that is not sure gets `certainty` `probable` or `possible`. An event gets `date_certainty` and `place_certainty` with the same values. Each of them takes a `certainty_note` with the reason.
7. Call `get_chart` to read the result. Show the user what exists and ask what is missing.
8. Upload photos and documents. Call `create_upload_urls`, send each file with HTTP `PUT` to its URL, then call `create_media` with the key and the `kind` (`photo` or `document`).
9. When the tree has persons, write the research rules of the tree with `update_guidelines`: which archives to use, how to cite, how to write names and places. When rules exist, pass the `version` from `get_guidelines` as `base_version`.
10. On a mistake, call `list_changesets` to find the batch and `revert_changeset` to undo it. With a `research` grant, `update_guidelines` and `revert_changeset` do not exist: skip step 9 and ask the admin to revert. A revert fails when later changes touch the same rows. Read the conflicts and fix them by hand.

## Rules

- One generation, then check, then the next.
- Names as the user says them. Keep the spelling of old records.
- Places as the user says them, for example "Musterdorf".
- Ask before you write a guess.
