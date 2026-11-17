# n8n Slack Recipe Bot - Social Eagle Week 3 Day 4 (Assignment 8)

An n8n automation that lives entirely inside Slack: a user types a recipe name
in a channel, an AI works out the products and ingredients needed, and the
workflow replies with the list in the same channel.

## The workflow

Slack Trigger -> Edit Fields (capture the recipe name) -> Basic LLM Chain
(generate the ingredient list) -> Code (format neatly for Slack) -> Slack
(Send Message back to the same channel).

## Setup

1. Create a Slack app/bot at api.slack.com with permission to read and send
   messages (`channels:history`, `chat:write`, `app_mentions:read`), install
   it to your workspace and invite the bot to your test channel.
2. In n8n: Workflows -> Import from File -> `workflow.json`.
3. Connect your Slack credential on the Slack Trigger and Reply nodes, and
   your AI provider credential on the OpenAI Chat Model node (a free
   OpenAI-compatible provider such as Groq also works in n8n).
4. Pick your test channel in both Slack nodes, activate the workflow, then
   type a recipe name (e.g. "Paneer Butter Masala") in the channel.

## Behaviour

```
User (in Slack): Paneer Butter Masala
Bot (in Slack):  To make Paneer Butter Masala you'll need:
                 - Paneer
                 - Butter
                 - Tomatoes, onions, cashews
                 - Cream, ginger-garlic paste, spices
```

An unclear or empty recipe name gets a polite "please rephrase" reply - the
prompt in the Basic LLM Chain node handles it.

Credentials stay inside n8n. Never paste API keys into nodes or commit them
to GitHub.
