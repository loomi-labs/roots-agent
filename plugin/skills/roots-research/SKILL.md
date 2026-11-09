---
name: roots-research
description: "Research a person or work on the research tasks of a roots tree: claim a task, search archives, log each search, propose the finds with sources, and write a report. Use when the user asks to research a person or to work on research tasks."
compatibility: Needs the roots MCP server (Streamable HTTP with OAuth).
metadata:
  scope: research
  tools: get_guidelines list_research_tasks claim_task get_context list_archives find_searches log_search search create_proposal submit_report
---

# Research with roots-research

This skill needs the `research` scope. In this scope you never write genealogy data directly. Each find goes into `create_proposal`, and an admin approves it.

## Steps

1. Call `get_guidelines` first. Follow its rules in every step.
2. Call `list_research_tasks`. Pick a task with the user, then call `claim_task` with the `task_id` and the `base_version` (the version from `list_research_tasks`).
3. Call `get_context` for the person of the task. It gives the relations, the events, the open tasks and the last searches.
4. Use `search` to find what the tree already holds about a name, a place or a source.
5. Call `list_archives` to see where to search.
6. Before each search, call `find_searches` for the person, the archive or the terms. Do not run a search two times.
7. Run the search. After each search, call `log_search`: the archive, the query, the result (`found`, `partial`, `nothing` or `blocked`) and a note. Log a search with no result too.
8. For a find, call `create_proposal` with the changes: the source, the citation and the new facts. Add a clear message.
9. At the end, call `submit_report` with the `task_id`, the `base_version` (read the task again with `list_research_tasks`) and the status of the task: `done`, `in_progress` or `dropped`. The report says what you did, what you found and the leads.

## Rules

- Cite each fact with a source.
- A guess about a person or a family gets `certainty` `probable` or `possible`. A guess about an event gets `date_certainty` or `place_certainty`. Each takes a `certainty_note` with the reason.
- A human check (a captcha, a login, a payment) is for the user. Stop and ask the user.
- Never invent a find.
