---
name: secondbrain
description: Use the user's Secondbrain workspace (daily notes, tasks, meeting recaps, documents, calendar and the Atlas of people, projects and organizations) whenever they ask about their own work — what was said or decided in a meeting, what is pending with someone, what they have today, what they did, who knows about something — or ask to note, remind, schedule, create or complete something. Answer from their data, not from general knowledge.
---

# Secondbrain

Secondbrain is the user's work memory. Its MCP server (the `secondbrain` connector in this plugin) exposes their workspaces as tools. The first time a tool is called, Claude asks the user to sign in to Secondbrain; after that, every conversation can read and write their workspace.

## Answering a question about their work

1. **Start with `recall`.** One call returns the most relevant passages (by meaning and by text), the Atlas wiki of the people and projects involved, their open tasks with the real status, and where they last came up. Without `workspace_id` it searches every workspace at once. Each result says in `abrir` which tool opens it in full.
2. **For a person, project or organization, read its wiki** (`get_entity_wiki`). It is the best summary that exists and it cites its sources.
3. **For typical requests there is a recipe.** `get_playbook` without arguments lists them: prepare a meeting, catch up on a project, what was decided, commitments with someone, my day, what I did, plan the week, close the day, and more. Follow the recipe: it names the tools and the order. The same recipes appear as the connector's prompts.
4. **Quick routes:** "what do I have today?" → `get_agenda`. "What did I do?" → `get_working_log`. "What's with Acme?" → `recall("Acme")`.

## Rules

- **Every claim comes from a tool, with its source next to it**: type, name and date, e.g. "(recap "Sync Acme", Sep 12)". If something is not there, say so instead of guessing.
- **Keep apart what was said, what was decided and what was done.** An action item from a recap is a proposal, not a task, until someone confirms it. A line in the daily note that looks like a task is provisional until confirmed.
- **Use canonical names.** Before creating anything with people or projects, find them with `search_entities`; writing a new name duplicates the Atlas.
- **Dates are in the user's time zone**, as `YYYY-MM-DD`. If you need "today" and don't know it, use `get_agenda` or ask.
- **When the user names a workspace** ("in Acme", "in my personal one"), everything in that request goes there: pass the name as `workspace_id`. If they have several and name none, ask before writing.
- **Write only when asked.** When the request is itself the order ("note that…", "remind me…", "create the task…"), do it and show what was saved. Otherwise show what you would change and wait for a yes. To change a document, use `patch_document` or `append_document`, never rewrite it whole.

## Vocabulary

- **Daily note**: one free-text note per day. Line markers mean something: `✅` declares a task, `🏁` a milestone, `📌` a decision, `⏰ 15:30 — …` a reminder. Closing the day processes what was written.
- **Task**: a real row with a status (pending, in progress, completed, cancelled) and a separate backlog. Assignee, related people and owner are three different things.
- **Recap**: a recorded meeting with transcript, summary and action items.
- **Atlas**: the knowledge graph — people, organizations, projects and tags — that links tasks, documents and recaps.
- **Reminder**: rings the phone at a time. It is not a task with a date.
- **Calendar**: local events are editable; events synced from Google, Outlook or Apple are read-only here.

Guide: https://www.onsecondbrain.com/guide/mcp
