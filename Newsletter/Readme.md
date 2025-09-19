# Agent Newsletter System (n8n) — Publish-Safe Export

This repository contains a sanitized n8n workflow that automates an AI newsletter pipeline:
- Weekly schedule
- Web research via Tavily
- Planning (title + exactly three topics)
- Per-topic section writing with real citations
- Final merge into an email-ready HTML newsletter
- Gmail draft creation


Important: This export is publish-safe; all credentials and personal identifiers are replaced with placeholders. You must insert your own credentials and emails in n8n.

## How it works (high level)
1. Schedule Trigger runs weekly.
2. Tavily fetches recent articles on your seed query.
3. Planner generates a title + 3 topics (schema-enforced).
4. Each topic is researched and turned into a standalone section with citations.
5. Editor merges the three sections into an HTML email with sources list.
6. Gmail node creates a draft ready to review and send.

## Setup Steps
- Import the JSON into n8n (Workflows → Import from file).
- Replace placeholders:
  - <REDACTED_TAVILY_CRED_ID>, <YOUR_TAVILY_ACCOUNT_NAME>
  - <REDACTED_OPENROUTER_CRED_ID>, <YOUR_OPENROUTER_ACCOUNT_NAME>
  - <REDACTED_GMAIL_CRED_ID>, <YOUR_GMAIL_ACCOUNT_NAME>
  - <RECIPIENT_EMAIL_PLACEHOLDER>
- Adjust the initial search query if needed (e.g., “AI adoption for small business”).
- Enable the workflow.

## Security Notes
- This JSON intentionally excludes secrets and personal data.
- Always review nodes for any environment-specific values before publishing or enabling.
