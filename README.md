# Secondbrain for Claude

Your work memory inside Claude. This plugin connects Claude to your
[Secondbrain](https://www.onsecondbrain.com) workspace — daily notes, tasks,
meeting recaps, documents, calendar and the Atlas of people, projects and
organizations — so you can ask what was said or decided, prepare a meeting,
plan the week, and write back without leaving the conversation.

It bundles:

- **The Secondbrain connector** — the remote MCP server at
  `https://api.secondbrain.media/functions/v1/mcp`. You sign in with your
  Secondbrain account the first time a tool is used (OAuth); there is no key
  to copy.
- **The `secondbrain` skill** — tells Claude when to reach for your workspace
  and how to answer from it: search first, cite the source of every claim,
  keep action items apart from tasks, and write only when you ask.

## Install

In Claude Code:

```
/plugin marketplace add agustindev/secondbrain-plugin
/plugin install secondbrain@secondbrain
```

The connector is also listed in the Claude directory, for claude.ai, Claude
Desktop and mobile.

## Try it

- "What did we decide with Grupo Andes last week?"
- "Prepare my 3 pm meeting."
- "What's due this week?"
- "Note in today's daily note that I'm sending the proposal."

## Links

- Guide: https://www.onsecondbrain.com/guide/mcp
- Privacy: https://www.onsecondbrain.com/privacy
- Terms: https://www.onsecondbrain.com/terms
- Support: https://www.onsecondbrain.com/contact
